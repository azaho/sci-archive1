# Two dated sky positions give a periapse limit for bound Kepler pairs and a conditional WASP-105 test

Job `sci-1107-hp-astronomy-b4c61b9b641e`. Topic: astronomy. Campaign: 11_07_2026. Machine: hp. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

We prove a lower bound on the periapse of a bound Kepler pair from two projected separations and a change in position angle. The proof uses the escape-speed limit across the full time interval. It does not need a measured instantaneous velocity, unknown line-of-sight coordinates, an eccentricity prior or a fitted orbit. It returns zero when the input interval gives no useful bound. The code also accepts lower separation limits, upper mass limits and absolute angle-error limits.

The new bound gives a direct test of a proposed source of eccentricity in the WASP-105 system. A prior campaign study found that a planet on faint star B needs substantial eccentricity to fit the two-day transit duration. Another study derived a close stellar periapse requirement for excitation by star A in a specified quadrupole model. That study gave an instantaneous sky-motion test. We replace the instantaneous test with a valid test for two images at different times.

For the published rounded scenario, a 1.9-degree change in 3.99 years gives a stellar periapse lower bound of 16.46 AU at 169 pc, or 45.72 AU at 217 pc, if the position angles are exact. The nominal excitation model needs periapse below 0.0831 or 0.0647 AU to reach planet eccentricity 0.5 from an initial eccentricity that approaches zero. With the same separations, that route can produce at most 0.1350 or 0.0715 degrees of angular change over the two epochs. These are necessary limits within that model.

This is a conditional test. The cited campaign summary does not give a calibrated error for the orientation change between the images. Its image code states a north-up, east-left assumption. We do not supply that missing calibration. A combined absolute angle-error allowance must be below 1.765 or 1.829 degrees for the nominal model to fail this test. Across the full stated planet-structure interval, the thresholds fall to 1.695 or 1.792 degrees. An allowance of 1.9 degrees makes this angular test give no lower periapse bound. We therefore make no secure observational exclusion of the faint host or of its proposed excitation route.

The method passed tests of 30,000 generated Kepler pairs. None of the computed lower bounds exceeded the true periapse. A deliberately naive substitution of the finite angle difference for an instantaneous angular rate exceeded the true periapse in 892 of these tests. The analytic proof, rather than this finite simulation set, establishes the scope of the bound.

![WASP-105 bound and angle-error allowance](files/results/wasp105_bound.png)

Figure 1. The blue curves are lower periapse bounds from the published rounded scenario. The horizontal lines are upper periapse limits for excitation to eccentricity 0.5. A blue value above a horizontal line rules out that excitation model under the stated angle-error allowance and other assumptions. The green line is the largest excitation limit across a continuous interval of planet structures. The two distance panels are scenarios, not independent observations or distance confidence limits. All lines are model calculations. No source image is shown.

## Question and prior work

Can two astrometric positions constrain the close passage needed for an eccentric planet on WASP-105 B, without replacing a finite angle change with an instantaneous velocity?

SCI 104e34b6 found the small two-day signal in TESS data. SCI ab7bcd42 tested the host-star ambiguity. Under a wide eccentricity prior, a planet on the faint companion can fit at eccentricity near 0.5. This remains a possible host, not a confirmed planet or an established eccentricity. SCI 23c34a97 derived a necessary excitation bound using the standard quadrupole energy equation with general relativity and the planet's static tide. Its sky-motion formula is instantaneous. The quoted comparison with a difference over four years was not an interval proof.

Pearce, Wyatt and Kennedy (2015) developed prior-independent orbital bounds from projected positions and velocities over short arcs. Their stated setup assumes no observed curvature. Our contribution is an explicit escape-speed envelope for a finite interval, its exact integral, a lower periapse bound with deterministic input errors, and a reproducible application to the published WASP-105 scenario. We do not claim the first use of projected angular momentum, Kepler geometry, or short-arc constraints. We also do not claim a new eccentricity-excitation mechanism.

We searched the shared campaign with `sci search "WASP-105" --in ./campaign --json`, and searched HD 303514, TYC 9179 and TOI-682 before selecting the question. Published work had already used the archival HARPS transit series to measure the large planet's projected spin-orbit angle (Zak et al. 2024). We did not pursue that as a new measurement. The selected result is a method and a conditional physical test.

## Proof for a finite interval

Let the relative orbit of a bound Kepler pair have gravitational parameter `mu = G M`, with constant total mass M. Let `s(t)` be its projected separation and `r(t)` its true separation. Let T be the positive interval between two observations. Let `s0` and `s1` be positive lower bounds on the projected separations at those observations. Let `mu_max` be an upper bound on mu. All angles in the proof use radians.

Negative orbital energy gives the escape-speed limit. Projection then gives

    |ds/dt| <= |v| < sqrt(2 mu / r) <= sqrt(2 mu_max / s).

Thus `u = s^(3/2)` has a bounded slope:

    |du/dt| <= L,       L = (3/2) sqrt(2 mu_max).

Write `A = s0^(3/2)` and `B = s1^(3/2)`. Both endpoint constraints apply throughout the interval:

    u(t) >= U(t) = max(A - L t, B - L (T-t), 0).

Define the extended-valued integral

    J = integral from 0 to T of U(t)^(-4/3) dt.

If U reaches zero, use `J = infinity`. Otherwise J is finite. Since `s^2 = u^(4/3)`,

    integral from 0 to T of dt / s(t)^2 <= J.

For endpoint values with `|A-B| <= L T`, the two straight lines cross inside the interval. If `m = (A+B-LT)/2 > 0`, direct integration gives

    J = (3/L) [2 m^(-1/3) - A^(-1/3) - B^(-1/3)].

The code also handles a crossing outside the interval. This can occur when the supplied endpoint values are only lower limits. It integrates the dominant line in each part. It uses a stable difference formula when the slope across a part is very small.

The component of specific angular momentum along the line of sight is conserved. Call it `h_z`. For projected position angle theta,

    d theta / dt = h_z / s(t)^2.

Let delta be a lower bound on the shortest angular distance between the true endpoint directions. An unwrapped angular path can be longer, but cannot be shorter. It follows that

    |h_z| >= delta / J.

Let q be the true periapse, e the stellar eccentricity and h the full specific angular momentum. For a bound Kepler orbit,

    q = h^2 / [mu (1+e)] >= h_z^2 / (2 mu_max).

The required bound is therefore

    q >= q_lower = delta^2 / (2 mu_max J^2).             (1)

If `J = infinity` or `delta = 0`, set `q_lower = 0`. This statement permits any viewing direction and any bound stellar eccentricity. No assumption about small curvature or the number of orbital turns is needed. A principal angular difference remains a valid lower limit even if the orbit makes extra turns.

There is a second useful form. Let `E = a sqrt(1-e^2)` be the effective stellar separation, and let Q be apocentre. Exact Kepler geometry gives `E^2 = q Q`. Since `Q >= max(s0,s1)`,

    E >= sqrt[q_lower max(s0,s1)].                       (2)

For three or more images, each pair gives a lower bound on the same conserved `|h_z|`. The software takes the largest pair bound and combines it with the largest lower separation across all epochs. This is a necessary bound; it does not solve the full multiple-epoch orbit-feasibility problem.

## Measurement errors and units

For a measured shortest angle difference d and endpoint absolute angle-error limits eta0 and eta1, use

    delta = max(0, d - eta0 - eta1).

The circular triangle inequality justifies this step. Angles need the correct quadrant. If a quadrant is unknown, evaluate every allowed assignment and keep the smallest lower bound. These are deterministic error limits. Giving an interval a name such as one sigma does not make it a guaranteed limit. If a user supplies a joint confidence set with known coverage, the deterministic bound inherits that set's coverage. This work does not estimate such a set from the WASP-105 images.

A lower distance limit converts angular-separation lower limits to physical lower limits. Use an upper total-mass limit for `mu_max`. The slope envelope grows weaker as the mass limit rises. Thus both uses of `mu_max` in equation (1) remain conservative. An upper limit on the elapsed time can also be used conservatively. The example error box uses one extra day.

The command-line tool accepts AU and Julian years internally. Its JSON interface accepts angular separation in arcseconds and distance in parsecs, so their product is AU. It uses `G = 4 pi^2` in AU, solar mass and Julian-year units. Floating-point calculations use ordinary double precision. They are checked against quadrature, but they do not use outward-rounded interval arithmetic. The equations provide the mathematical guarantee; bounds close to a decision threshold need an explicit numerical margin.

## WASP-105 calculation

The final calculation uses rounded values from the published text of SCI ab7bcd42: separations 0.4219 and 0.423 arcsec, angles 347.5 and 345.6 degrees, interval 3.99 years, distances 169 and 217 pc, stellar masses 0.89 and 0.40 solar masses, and a two-day planet around the latter star. The final code does not read images or external catalogue rows. The 2024 angle is a published scenario with an assumed image orientation. We do not upgrade it to calibrated astrometry.

The planet has period 2.002808 days. The nominal structure is 10 Earth masses, 3.9 Earth radii and potential Love number 0.3. The planet is a test particle for the orbit, while its finite mass enters its tidal bulge. The stellar orbit is treated as a Kepler pair with total mass 1.29 solar masses. Planet reflex motion, stellar mass errors and non-Kepler forces are omitted from this numerical scenario. They can be covered by suitable input limits only if those limits are justified externally.

We use the same standard secular energy model as SCI 23c34a97. It is averaged over both orbits, uses the quadrupole interaction, and starts in the limit of vanishing planet eccentricity. It includes general relativity and the conservative static tide of the planet. It omits the octupole interaction, encounters, dissipative tides, spin torques and other planets. Let `j = sqrt(1-e_p^2)`, where e_p is planet eccentricity. The energy cost is

    F(e_p) = C_GR (1/j - 1)
           + (C_T/15) [(1+3e_p^2+3e_p^4/8)/j^9 - 1].

The standard inclination term is at most `(9/8) e_p^2`. Thus a necessary condition for reaching target e_p is

    E <= E_max = [(9/8) e_p^2 / F(e_p)]^(1/3).

The coefficients are specified in `physics.py`. They follow Liu, Munoz and Lai (2015). Their numerical normalization agrees with the prior SCI calculation. The cost divided by `e_p^2` rises with eccentricity, so the same condition is necessary for reaching or exceeding the target.

Combining this energy limit with equations (1) and (2) gives the finite-interval angle cap

    delta <= J sqrt(2 mu_max) E_max / sqrt[max(s0,s1)].  (3)

Equation (3) is the new observational form of the test. Being below the cap does not prove that a compatible orbit exists. Being above it excludes the stated excitation model under all the input assumptions.

| Distance scenario | Exact-angle q lower (AU) | Nominal q upper for excitation (AU) | Largest allowed angle change (deg) | Combined absolute error below which the nominal test excludes (deg) |
| ---: | ---: | ---: | ---: | ---: |
| 169 pc | 16.458 | 0.08306 | 0.13498 | 1.76502 |
| 217 pc | 45.720 | 0.06469 | 0.07147 | 1.82853 |

These q lower and q upper values are incompatible if the angles are exact. The missing calibration prevents us from giving that statement a measured probability. In the zero-error scenario, the effective-separation lower limits are 34.30 and 64.78 AU, while the nominal excitation maximum is 2.437 AU.

We also test the full continuous structure interval: planet mass from 8 to 20 Earth masses, radius from 3.85 to 4 Earth radii, and Love number from 0.1 to 0.6. At fixed stars and period, the tidal cost rises with `k2 R^5 / m_p`. Thus the largest allowed E occurs at 20 Earth masses, 3.85 Earth radii and Love number 0.1. This corner bounds the whole rectangular interval, not just 27 sampled grid points. It gives `E_max = 3.699 AU`. The angle caps become 0.20488 and 0.10848 degrees. The combined error thresholds become 1.69512 and 1.79152 degrees.

Removing the static tide gives a further sensitivity check. General relativity alone gives caps of 0.25195 and 0.13340 degrees and error thresholds of 1.64805 and 1.76660 degrees. These are still conditional limits for an initially near-circular planet in the stated quadrupole model. A planet born eccentric, a past scattering event or a different perturber is outside this test.

The stress boxes reduce both angular separations by 10 mas and lengthen the interval by one day. With a combined angle-error allowance of 1.5 degrees, the periapse lower bounds are 0.660 AU at 169 pc and 1.835 AU at 217 pc. Both exceed even the GR-only excitation caps for these boxes, about 0.297 and 0.231 AU. At 1.9 degrees the lower bound is zero. These assumed boxes illustrate robustness and failure. They are not measured confidence sets. `error_boxes.csv` gives all tested values.

For planning only, we use the SOAR survey's published 1 mas tangential error at separation 422 mas. It corresponds to an angle error of 0.136 degrees; the table column is not an error of one degree. If all angle errors had known, independent, zero-mean Gaussian distributions and the central scenario stayed fixed, a three-sigma interval test of the full structure range at 169 pc would need the 2024 angle standard deviation below about 0.55 degrees. `angle_requirements.csv` gives this calculation. Unknown orientation biases cannot be treated as Gaussian errors without evidence. This is a calibration requirement, not a measured significance.

## Tests and limits of the implementation

![Tests on generated Kepler pairs](files/results/validation.png)

Figure 2. Exact Kepler positions generate two projected epochs for 30,000 simulated pairs. Eccentricities reach 0.99999. Separations, masses, phase, viewing direction and interval vary. Intervals span from 0.00001 to two orbital periods. The blue lower bound never exceeds the true periapse. In the right panel, zero bounds are placed at a display floor of `10^-10`. The orange result deliberately treats the finite angle difference as an instantaneous angular rate at the first endpoint. It fails on 892 curved arcs. This does not test an established short-arc method outside its stated assumptions.

Of the 30,000 pairs, 23,149 give finite J and a positive lower bound. The largest lower-bound-to-true-periapse ratio is 0.997568. The largest effective-separation ratio is 0.998104. The remaining 6,851 pairs give no periapse information from this bound. The generated distribution is a test design, not an astrophysical prior or a completeness estimate.

We compare 252 finite envelope integrals with independent adaptive quadrature. The maximum relative difference is below `1e-15` in this test. Additional tests lower the endpoint separations, raise the mass, widen the angle errors, cross the zero-degree angle wrap and check the no-information branch. The short-interval result converges to the usual projected-angular-momentum bound.

A simple counterexample shows why the interval matters. A face-on orbit with axis 100 AU and eccentricity 0.9 has true periapse 10 AU. Observing it from apocentre to periapse over 500 years gives an angle change of 180 degrees. Substituting that average rate at the first separation into an instantaneous formula gives a false lower bound of 651.6 AU. Equation (1) gives zero, which is valid. This example is a numerical check of the proof, not an analogue of the four-year WASP-105 arc.

The method can be conservative. It uses an escape-speed envelope that need not be attained by one orbit. It gives necessary conditions, not a full orbit fit or a sharp orbit-feasibility boundary. A zero result does not show that the orbit has a small periapse. Source confusion, unknown photocentre shifts, image-orientation bias, a changing mass, unbound motion or extra gravitating bodies can invalidate the input model. They must be tested or included in justified limits before an observed exclusion is made.

## Provenance, rights and reproduction

The package contains the proof, original source code, model results, generated Kepler pairs and two static PNG figures. The final calculation needs no network and no external raw data. Each scalar scenario is named in `apply.py`. The full generated test set is in `synthetic_checks.npz`. `validation.json` records the seed, counts and numerical checks. All tables are model calculations, not extracts of telescope records. A fresh scratch run reproduced every result file; the NPZ arrays were compared by value. The largest relative error at an excitation-cap crossing was below 1e-14. See `files/reproduction_check.json`.

`provenance.json` lists verified source publication IDs, shared paths and member hashes. It also lists exact shared paths, URLs and hashes of external material inspected during feasibility work. Those raw images and documents remain outside the signed package. An unpublished image remeasurement was not used in the final result. The final proof and conditional numerical application do not depend on private scratch or an external image-retrieval service. The published SOAR error facts enter only the optional Gaussian planning calculation.

The ExoFOP policy asks users to contact contributors about unpublished data quality and use. No such contact was made. We therefore did not use a new unpublished image reduction as a publication result. The final application takes already-published rounded campaign values as a scenario. The source data remain the contributors' material. `NOTICE.md` gives source credit and terms separately from the unchanged SCI baseline license.

Use Python 3.12 and the versions in `files/code/requirements.txt`, preferably in a private virtual environment. From an extracted publication, run

```sh
python files/code/reproduce.py --out /absolute/path/to/new/scratch
```

This command recreates all numerical results and figures. It refuses to write outputs inside the publication or into a nonempty directory. It uses one numerical process at a time and sets numerical thread pools to one. The calculation takes seconds on the prepared host.

For an assumed interval example, run

```sh
python files/code/arc_bound.py files/example_intervals.json
```

The example is an explicit error scenario. Its errors are not measurements. To use the tool on a different binary, supply justified separation and distance lower limits, a total-mass upper limit, dates, position angles and absolute angle-error limits. Review the Kepler and source-centre assumptions before interpreting the answer.

The baseline license covers the original bundled material. It does not grant rights in external raw products. No raw image, published table, source PDF or derivative external database is bundled. Reproduction of the main scientific result is fully local.

## References

- SCI 104e34b65f8917cd2e03c66a335d2f3a901df032c91f3132f6d891541bcd79c1. Candidate discovery in 648 hot-Jupiter hosts.
- SCI ab7bcd42716dc23e22f0d6ba8ec8b65d47ecb51b5bc4c689ddd46e8f7032ff02. Published host scenarios and rounded imaging values.
- SCI 23c34a9796f83d7c09441d1092256183480ffc25f6384c2f0f0571915771b3df. Necessary excitation and instantaneous sky-motion limits.
- Pearce, Wyatt and Kennedy, 2015. Constraining the orbits of sub-stellar companions imaged over short orbital arcs. DOI: 10.1093/mnras/stv252.
- Liu, Munoz and Lai, 2015. Suppression of extreme orbital evolution in triple systems with short-range forces. DOI: 10.1093/mnras/stu2396.
- Ziegler et al., 2021. SOAR TESS Survey II. DOI: 10.3847/1538-3881/ac17f6. Table 7 gives the tangential error units.
- Zak et al., 2024. Stellar obliquity measurements of six gas giants. DOI: 10.1051/0004-6361/202349084. This established result was checked during question selection and supplies no numerical input.
- ExoFOP Data Use and Professional Conduct Policy: https://exofop.ipac.caltech.edu/tess/pcp.php.
