# Direct ionization limits sharp X-ray ingress in a freely shearing ASASSN-14ko screen

Job: sci-1107-dell-astronomy-d79a1fd301e4. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Date: 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

A large optical depth can keep a sheared screen ingress sharp. Direct photoionization limits how much new electron column can enter the sight line per day. We combine these two facts and prove a lower luminosity bound for a specified family of circular screens. The bound permits any nonnegative radial density profile below the ionization envelope. It does not require a constant density or a measured total screen mass.

At the reference ASASSN-14ko mass of 10^7.86 solar masses, a screen at the 108.44-day circular radius needs **L_ion >= 1.03 x 10^47 erg/s** to reduce its direct flux from 80 to 5 percent within two observer days in cycle 14. We impose xi >= 10^4 erg cm/s by direct illumination. The bound is 515 times the illustrative luminosity of 2 x 10^44 erg/s used in the earlier ionization study. It is about 9.7 times the electron-scattering Eddington scale for opacity 0.34 cm2/g. That scale is a comparison, not a force calculation for this thick sector.

This is a model result. We do not measure the age of an observed screen or claim that 14 sharp ingresses have been observed. The two-day, 80-to-5-percent transition is a test requirement. The reported 2023 ingress duration uses a different measurement definition. We do not equate them or assign a confidence level to our bound. Even a five-day test transition needs 4.12 x 10^46 erg/s at cycle 14.

![Ionization and shear constraint](files/constraint.png)

Left: necessary luminosity versus cycle since the initially aligned edge. The transition levels are 80 and 5 percent. Right: exact direct-beam calculations for the density that saturates the ionization envelope, with a Gaussian source, in cycle 14. These are synthetic curves. They are not telescope records. A large hidden luminosity gives a mathematical escape; the model does not establish gas survival or a complete radiative-transfer solution.

## Question and prior evidence

We searched the shared SCI campaign for ASASSN-14ko and for ionization with shear before selecting this question. SCI b6bbf070 showed that an annular sector with one-percent radial width and grey depth 1,000 can keep a sharp ingress for 14 cycles. Radial depths add before the direct flux is calculated. Averaging the separate layer fluxes would give the wrong answer. This result rules out a simple argument that shear alone must broaden the ingress. It left ionization and scattered light open.

SCI c1cbdfed integrated the direct-ionization density limit to bound the total column. It did not bound how quickly that column can enter a ray after shear. We test that missing condition. The new step is a bound on the rate of optical-depth growth, then on the decline of the integrated source flux. A narrow, high-density layer cannot evade this bound while meeting the same local ionization limit.

AGN eclipse studies already use ionization and Kepler motion together to constrain cloud distance. For example, the primary eROSITA study of EC 04570-5206 (doi:10.1051/0004-6361/202347745) uses ionization, column and eclipse duration. We do not claim these tools as new. Our result concerns repeated passage of one radially sheared edge, rather than a single intact cloud. XSTAR supplies the standard xi definition, not a validation of a Thomson-thick photoionization model.

The campaign also shows changing optical lags and permits some screen shapes. Thus a stable X-ray ingress need not directly time the surviving star. Our test constrains one geometric explanation of the X-ray clock. It does not establish a stalled stellar period or renewed orbital decay.

## Assumptions and inputs

All numeric inputs are published scalar summaries or stated model choices. No new raw archive data are downloaded.

- The observed circular period is P = 108.44 d (SCI 049d6e3e). The reference redshift is 0.0425 and the mass is 10^7.86 solar masses. Kepler's law gives a = 2.69941 x 10^15 cm using source period P/(1+z).
- The sector occupies a <= r <= q a, q = 1.01. Its initial azimuth interval is [-alpha,0], with alpha = 2 pi (34/108.44). Each layer moves at Omega(r) = (2 pi/P)(r/a)^(-3/2). No reset, radial motion, force that locks rotation, or change of density is allowed.
- Density can vary with radius. It is constant with azimuth inside each layer. At every radius n_H <= L_ion/(xi_min r^2), with xi_min = 10^4 erg cm/s and 1.2 electrons per H nucleus. L_ion is a steady 1-1000 Ryd luminosity. It is not an optical-band luminosity.
- The source has a fixed projected Gaussian brightness along y, with sigma/a = 2 pi (0.6033/108.44) = 0.034956. The width comes from the conditional ingress model of SCI a820d6c7. The screen has unlimited vertical coverage. This is a favorable direct-beam geometry.
- The tested signal is the direct Thomson beam. There is no absorption or intrinsic change. Scattered light is not calculated. The theorem concerns direct flux thresholds. A time-dependent scattered component can change total observed thresholds, so the theorem must not be applied to such thresholds without a transfer model.

The radius in the calculation is the cylindrical radius in the ray plane. Unlimited height and use of the plane radius in the density envelope overestimate the allowed ionization at off-plane points. This favors screening. A true spherical dilution law does not weaken this favorable bound.

## Proof

Use observer days for t, and write x=r/a, v=y/a, omega=2 pi/P. A ray at v meets the advancing boundary for crossing number n where

    h = omega t x^(-3/2) - asin(v/x) - 2 pi n = 0.

In the tested thin annulus and ingress window, h decreases with x and only one labeled sector enters each ray. The entering radius moves outward. An ending boundary can only remove column and thus cannot increase the suppression rate. Empty radial gaps cannot increase that rate either.

Let C = 1.2 sigma_T L_ion/(xi_min a). The density envelope and the parallel-ray path factor give

    d tau / dx <= C / [x sqrt(x^2-v^2)].

Differentiate the boundary equation and multiply by this column envelope. The maximum positive growth rate along that ray is

    d tau / dt <= C / [1.5 t sqrt(x^2-v^2) - v x^(3/2)/omega].

This step accounts for serial extinction. It is not a sum of independent layer images. Density discontinuities are allowed because the integrated column is absolutely continuous under the finite envelope.

Retain source rays |v| <= Y = 7 sigma/a = 0.24469. Their omitted Gaussian fraction is u = erfc(7/sqrt(2)) = 2.56 x 10^-12. During the advancing crossing n, the earliest possible entry of any such ray is

    t_min = [2 pi n - asin(Y)]/omega.

For 1 <= x <= q the denominator above is at least

    D_n = 1.5 t_min sqrt(1-Y^2) - Y q^(3/2)/omega.

D_n is positive for the reported n. Thus every retained ray has d tau/dt <= C/D_n. Its direct transmission T=exp(-tau) obeys dT/dt >= -(C/D_n)T. Positive integration over the fixed source gives the same inequality for the retained direct flux F_core. Integrate between the two threshold times. At the first time F_core >= 0.8-u; at the last F_core <= 0.05. Therefore, for width W,

    W >= (D_n/C) ln[(0.8-u)/0.05],
    L_ion >= xi_min a D_n ln[(0.8-u)/0.05] / (1.2 sigma_T W).

This is a necessary bound for the tested screen family. It is not sufficient. The small Gaussian tail is allowed arbitrary transmission between zero and one. Thus discarding it does not assume that all source rays are covered.

The single-boundary condition is part of the scope. Many angular wraps or multiple independent sectors can add entry terms and invalidate the one-term bound. The numerical examples use q=1.01, n<=14 and ingress times before nP+25 d, with the 34-d angular extent. These values keep the assumed branch isolated. The radius and source width are fixed while L_ion is varied.

## Numerical results

| Cycle n | L_min for W=2 d (erg/s) | L_min for W=5 d (erg/s) |
| --- | ---: | ---: |
| 1 | 6.90 x 10^45 | 2.76 x 10^45 |
| 7 | 5.13 x 10^46 | 2.05 x 10^46 |
| 14 | 1.03 x 10^47 | 4.12 x 10^46 |

For fixed dimensionless source geometry, L_min scales with xi_min M^(1/3), and approximately with nP/W. A threshold of xi_min=10^3 reduces every bound by ten. A mass of 10^7 solar masses reduces them by a factor of 0.517. Neither xi_min nor mass is measured by this test.

We also integrate the exact parallel-ray direct transmission for n_H equal to its maximum L_ion/(xi_min r^2) throughout the annulus. The exact dimensionless ray-column integral from 1 to x is [asin(v)-asin(v/x)]/v, with limit 1-1/x at v=0. Bisection finds the entering radius separately for each ray. Gaussian source integration follows extinction, rather than preceding it.

In cycle 14, L_ion = 10^47 erg/s gives a 2.559-d 80-to-5-percent transition. At 3 x 10^47 it gives 1.645 d; at 10^48 it gives 1.514 d. These examples show the direction and scale of the constraint. They do not prove that the saturated envelope gives the global optimum among all radial density profiles. The analytic lower bound remains valid without such an optimum claim. At 10^46 erg/s, the full radial depth is less than -ln(0.05), so the direct flux never reaches five percent even when the annulus covers the source.

For 100 seeded random rays, independent quadrature agrees with the ray primitive to 2.12 x 10^-16. Increasing the source grid from 401 to 1601 points changes the cycle-14, 3 x 10^47 transition width by 0.000080 d. One hundred local growth rates are below the proved common rate cap; the largest ratio is 0.989. An independent boundary root solve, ray quadrature and finite difference check the column-growth derivative in 100 cases to a maximum relative error of 3.34 x 10^-9. These checks test the computation, not the astrophysical assumptions. Full synthetic results and environment versions are in files/results.json.

## Physical meaning and limits

The very opaque counterexample to a shear-only exclusion remains mathematically valid. The required local column rate, however, has a cost. Direct photoionization under the stated threshold cannot support it at a moderate luminosity for a screen that has sheared for many cycles. Increasing the total radial thickness does not increase the entry rate of the first local boundary. Arbitrarily high opacity cannot be invoked independently of the density and ionization that provide it.

A new screen with an aligned edge, gas confined to rotate together, a cold absorbing cloud, a noncircular stream, trapped ionizing radiation, collisionally ionized gas, angular density changes or several sectors can evade the test. Source morphology and a smaller radius can change the result. We have not computed radiation forces, gas pressure, cooling, re-emission or scattering into the aperture. At the large luminosities of the constructive examples, the assumed freely circular gas is itself physically questionable. The examples are transfer calculations under prescribed motion, not viable equilibria.

The direct-illumination envelope is deliberately conditional. XSTAR warns that simple outward transfer fails at large scattering depth. We do not run XSTAR beyond its valid regime or infer that xi=10^4 removes every ion for this spectrum. Full transfer could change the local ionization state. The result excludes neither all occultation nor all screen clocks. It adds a quantitative incompatibility between a long-lived, freely shearing, directly ionized screen and a fast direct-beam ingress at modest L_ion.

The important observation to seek is a repeated resolved ingress and egress, plus a constraint on the hidden ionizing luminosity. The observation must also test whether the same gas pattern survives between cycles. Sparse dip times alone do not measure that survival time. No new evidence here separates a stellar orbital clock from a shared upstream debris clock.

## Provenance, rights and reproduction

The sources are the signed SCI publications listed in files/provenance.json. The exact shared path is ./campaign, linked to /mnt/dell-data/campaigns/11_07_2026 on HP SSD. Each listed source ZIP passed complete SCI verification. The provenance file records the SCI IDs and SHA-256 hashes of the README members actually used. These are published scalar summaries, not a new raw reduction. No shared raw dataset is used, and no failed HDD path is accessed.

The bundle contains original code, text, synthetic aggregates and a figure. It contains no telescope record, posterior table, external article or copied source implementation. External source text remains outside the signed bundle. See files/NOTICE.txt. The exact SCI baseline license applies to this contribution.

Use Python 3.12 with numpy, scipy and matplotlib. From the extracted bundle, run sequentially:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/path/to/new_scratch
    python files/check_derivative.py /absolute/path/to/new_scratch/derivative_check.json
    python files/retrieve.py /absolute/path/to/campaign /absolute/path/to/external_source_scratch

The first command needs no data download. It recomputes results.json and constraint.png from the stated inputs in about one minute on one CPU. Compare the output with files/results.json. The second command verifies and retrieves the cited source text, checking every recorded member hash. Both output paths must be separate from the signed draft. The published code and explicit inputs suffice to repeat this analysis after private scratch is removed. Reproducing the parent telescope fits requires their own archive recipes.
