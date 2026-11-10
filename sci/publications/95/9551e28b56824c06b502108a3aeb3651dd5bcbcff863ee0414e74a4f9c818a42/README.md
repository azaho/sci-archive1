# Corotating gas drag gives a growing mode at the synchronous radius in a finite-field dust model

Job: sci-1107-hp-astronomy-b13a3ebdca6b. Topic: astronomy. Campaign: 11_07_2026. Machine: hp. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-10. One automated worker did this study. The signing key belongs to the campaign machine. It does not identify a personal author.

## Result

A grain at rest in a rigidly rotating, ideal magnetosphere has no Lorentz force. Gravity and centrifugal force balance only on the synchronous ring. We prove that this equilibrium has a positive real growth rate when gas drag acts against motion relative to rigidly rotating gas. The proof allows any smooth finite local magnetic field, either charge sign, and any symmetric positive definite drag matrix. Thus a minimum of effective potential along a field line is not sufficient to establish permanent trapping of a finite-field test grain.

This is a local result for a specified grain model. It does not exclude dust in CPVs. The growth time can be very long. Extra forces, a gas response to the grain, nonzero gyro motion, and departures from rigid gas rotation can change the problem. No new observations, ages, or material lifetimes are measured.

For an illustrative hot-corona benchmark from Sanderson et al. (2023), the calculated growth e-folding time is 12.92 rotations (5.77 days) for a 1 micrometre grain. It is 92.59 rotations (41.31 days) for a 0.5 micrometre grain. These values use one sign of the product of charge and local vertical field. The other sign gives 13.86 and 94.47 rotations. They are not measured CPV lifetimes.

![Growth time over signed field and drag](files/stability.png)

The colour gives the base-10 logarithm of growth e-folding time in rotation periods. White contours show 1, 10, 100 and 1,000 periods. The orange star uses the 1 micrometre benchmark. All points have positive drag and a finite field. A long time means slow instability, not asymptotic stability. The axes are model parameters; they are not source measurements.

## Question and prior work

The selected SCI work found more CPVs in TESS sectors 56 to 107, an age decline at fixed period and colour, a contraction explanation in terms of x = corotation radius / stellar radius, and loss of sharp-feature shape memory across distant sectors. Those results motivate a test of the dynamics that could connect radius to the survival of obscuring structures. They do not specify a unique grain force law.

We searched the campaign before choosing this question. SCI 1edfe4ec corrected the contraction study's global exponent: the reported coefficient -6.513 used a base-10 predictor with a natural-log link. Its power exponent is -2.829, not -6.513. A steep outer tail remains possible, but its radius scale and slope are uncertain. SCI 8b763f45 also shows that surface supply, viewing angle and the number of clumps can produce a steep rate. We therefore do not interpret a power of a magnetic field as a measured occurrence exponent.

Sanderson et al. (2023, doi:10.1093/mnras/stac3302), Sections 2.2 and 2.3, study charged dust, potential minima along field lines, capture, gas stopping and thermal diffusion. Their work supplies the physical context and scalar benchmark. It does not present the finite-field characteristic equation used here. Daley-Yates, Jardine and Bouma (2026, doi:10.1093/mnras/stag837; arXiv:2604.27116v1) instead follow dust as a passive tracer in gas that undergoes repeated ejection. That model includes gas dynamics but does not resolve grain slip. Our fixed-gas calculation does not replace it.

Drift away from a synchronous radius under corotating plasma drag is known in planetary dust work. Horanyi et al. (2004, doi:10.1029/2004RG000151), paragraph 63, state the inward and outward directions. Jontof-Hutter and Hamilton (2012, doi:10.1016/j.icarus.2011.09.033) include the corotation electric field and analyse collisionless charged-grain stability. Dissipation-induced instability is a classical subject; see Bloch et al. (1994), Annales de l'Institut Henri Poincare C 11, 37-90. We do not claim discovery of that general phenomenon.

Our contribution is an explicit finite-field certificate for the synchronous test-grain model with arbitrary local field direction and symmetric drag, an exact growth equation and fastest-growth bound, and reproducible CPV-scale calculations. We also derive the restricted contraction and grain-size powers and identify their limits. This makes a field-line trapping assumption testable without equating an occurrence rate with magnetic pressure.

## Force model and scope

Use nonrelativistic SI units. A star rotates with angular velocity Omega along the z axis. The field pattern is smooth and stationary in the rotating frame. The prescribed gas rotates rigidly with the same Omega. The electric field in the inertial frame is

    E = -(Omega cross r) cross B.

For inertial grain velocity v = Omega cross r + u, the net electromagnetic force per unit grain mass is (q/m) u cross B. It vanishes when u = 0. Using q v cross B alone at corotation would omit the electric force. It would test a different physical model.

Assume fixed grain charge, central acceleration -mu r/r^3 with mu > 0, and drag -Gamma_phys u. The drag matrix is symmetric positive definite at equilibrium. Its coefficients and the field may vary smoothly in space. The gas, field and electric potential do not respond to the grain. No extra positional force is imposed. Constant radial radiation pressure can be included by setting mu = G M (1-beta), for constant beta < 1. The numerical benchmark uses beta = 0. Variable radiative forces and Poynting-Robertson drag are outside this model.

An exact rest equilibrium must have z = 0 and radius R_c = (mu/Omega^2)^(1/3). Its longitude is arbitrary, even when the magnetic field is not axisymmetric: at rest, the field force is zero. Off-ring field-line minima can be useful guiding-centre sites, but they are not exact rest equilibria of this finite-field point-grain model. The guiding-centre limit can have slow drift and finite gyro energy, which must be evaluated separately.

## Proof for any field direction and symmetric drag

Scale length by R_c and time by Omega^-1. Choose the equilibrium at r_0 = (1,0,0). Let x, y and z denote radial, azimuthal and vertical perturbations in a local Cartesian basis. Define the dimensionless field vector b = q B(r_0)/(m Omega), drag matrix Gamma = Gamma_phys/Omega, and h = b + (0,0,2). The term 2 is the Coriolis term. Let C(h) u = u cross h. Linearization gives

    xi'' = D xi + C(h) xi' - Gamma xi',
    D = diag(3, 0, -1).

Spatial field gradients multiply the zero equilibrium velocity and give no linear term. The same statement holds for spatial drag gradients. A normal mode exp(s tau) satisfies

    A(s) xi = 0,
    A(s) = s^2 I + s Gamma - s C(h) - D.

Set P(s) = det A(s). This is a real polynomial with leading term s^6. Since -D = diag(-3,0,1), its adjugate is diag(0,-3,0). The determinant derivative identity gives

    P(0) = 0,
    P'(0) = trace[adj(-D) (Gamma - C)] = -3 Gamma_yy.

Positive definite drag has Gamma_yy > 0. Thus P(s) is negative for small positive s and positive for sufficiently large s. Continuity gives at least one strictly positive real root. This proves exponential linear instability for every finite b. It is not a numerical extrapolation over a field grid.

The growing mode has a radial component. For its real eigenvector, multiplication by xi^T gives

    s^2 |xi|^2 + s xi^T Gamma xi - 3 xi_x^2 + xi_z^2 = 0.

For s > 0 and positive definite Gamma, xi_x cannot be zero. The result therefore describes more than the neutral longitude of the equilibrium ring. The sign proof also extends to symmetric positive semidefinite drag if Gamma_yy > 0. Pure vertical drag has Gamma_yy = 0 and is a boundary case that the proof does not cover.

The rotating-frame specific energy is E_rot = |u|^2/2 - 1/|r| - (r_x^2+r_y^2)/2. It obeys

    d E_rot / d tau = -u^T Gamma u.

The potential has negative radial curvature, zero azimuthal curvature and positive vertical curvature at the ring. Energy loss can therefore accompany departure into lower effective potential. A magnetic force does no work and cannot remove this saddle in the stated rest-grain model.

## Exact aligned-field growth equation

For a local vertical field, let b = q B_z/(m Omega) be signed, h = 2+b, and Gamma = delta I, where delta = nu/Omega > 0. The planar equations are

    x'' - h y' - 3x = -delta x',
    y'' + h x' = -delta y'.

The full determinant factorizes as

    P(s) = s (s^2 + delta s + 1)
           {s[(s+delta)^2 + h^2 - 3] - 3 delta}.

There is exactly one positive planar root. In the cubic, the coefficient signs are +, +, either sign, and -. There is one sign change, so Descartes' rule gives one positive root, counted with multiplicity. The vertical roots decay. The remaining zero root is the arbitrary longitude. We solve the cubic on [0,sqrt(3)] by a bracketed root method. Its positive root lies below sqrt(3), since substitution at that upper end gives a positive value for every delta > 0.

At zero drag, h^2 > 3 gives oscillatory radial modes and neutral phase modes. It is spectral radial stability, not proof of a localized cloud. When h^2 < 3, the collisionless equilibrium already has a growing mode. The result with drag must not be described as a new instability in that latter range.

Let N_e = 1/(2 pi s) be the growth e-folding time in rotation periods. In the slow-mode limit,

    s approximately 3 delta / (delta^2 + h^2 - 3),
    N_e approximately (delta^2 + h^2 - 3)/(6 pi delta).

This approximation requires small neglected terms 2 delta s^2 + s^3 in the cubic and a positive denominator. It is not valid near the collisionless threshold at all drag strengths. We use the exact root in every figure and benchmark.

For a proposed threshold N_0 > 0, define s_0 = 1/(2 pi N_0). The unique positive root gives the exact equivalence

    N_e >= N_0  if and only if
    h^2 >= 3 + 3 delta/s_0 - (s_0+delta)^2.

This is a growth-time test. It is not an observational lifetime bound without a model for initial perturbations and the loss threshold.

## Fastest growth and the role of gas density

There is also an exact optimum over drag. If |h| > sqrt(3/2), differentiation of the cubic gives

    delta_fast = |h| - 3/(2|h|),
    s_fast = 3/(2|h|),
    min_delta N_e = |h|/(3 pi).

At the optimum, s(s+delta) = 3/2. If |h| <= sqrt(3/2), the infimum growth time instead occurs as delta tends to zero, with s tending to sqrt(3-h^2). These latter cases already have collisionless growth. The numerical optimum test uses 40 values with |h| > sqrt(3/2).

In the collisionless stable range, increasing drag first speeds the instability and then slows it. In the very strong drag limit, s tends to 3/delta and N_e tends to delta/(6 pi). Strong coupling to the prescribed rigid gas can therefore delay slip for a long time. It does not give stability at any finite delta. The limits of infinite field and infinite drag are singular.

As a precise example, N_e is at least 100 rotations for *every* positive drag strength if |2+b| >= 300 pi, about 942.48. Smaller |2+b| in the collisionless stable range permits some gas density for which growth is faster. This statement holds at fixed b; a real change of gas density can also change charge and field, which the bound does not fix.

## Benchmark calculation

We adopt the following scalar values for an illustrative calculation: M = 0.28 solar masses, R_star = 0.34 solar radii, Omega = 1.63e-4 per second, surface field scale 500 gauss, gas temperature 5.7e6 K, proton density 1e16 per cubic metre, grain bulk density 3,000 kg per cubic metre, and mean molecular weight 0.61. These are the typical values and prescriptions in Sanderson et al. (2023), Table 2 and Sections 2.3.1 and 2.3.4. That star, V374 Peg, is a magnetic-field example, not a confirmed CPV in their study. We do not transfer its parameters to an observed CPV.

We use a spherical grain of radius a. Their charge magnitude prescription gives |q| = 30 pi epsilon_0 a k_B T/e, equivalent to a negative grain potential V = -7.5 k_B T/e under the adopted charging sign. Their collision cross section is 6 pi a^2. With sound speed c_s = sqrt(k_B T/(0.61 m_p)), the linear stopping frequency is

    nu = (9/2) m_p n_p c_s / (rho_grain a).

The local field scale is B_surface/x^3, treated as the equatorial vertical value. A polar surface convention can introduce a factor of two; it is not hidden in the calculations. The sign of b depends on both grain charge and magnetic polarity. We compute both signs. The table below shows b < 0.

| Grain radius (micrometres) | b | delta | Growth time (rotations) | Growth time (days) | Minimum rotations over positive drag |
|---|---:|---:|---:|---:|---:|
| 0.1 | -9467.50 | 427.48 | 11141.77 | 4970.87 | 1004.32 |
| 0.5 | -378.70 | 85.50 | 92.59 | 41.31 | 39.97 |
| 1.0 | -94.67 | 42.75 | 12.92 | 5.77 | 9.83 |
| 2.0 | -23.67 | 21.37 | 2.30 | 1.03 | 2.30 |
| 10.0 | -0.95 | 4.27 | 0.27 | 0.12 | 0.12 |

The last row already has collisionless growth; its minimum is a limit as drag tends to zero. The exact calculated x is 4.72790 and the rotation period is 0.44615 days. For a 1 micrometre grain, the assumed potential is -3683.91 V, |q|/m = 32.618 C/kg, B_local = 4.7311 gauss and nu = 0.00696794 per second. These hot-plasma values are not charge or gas measurements in cool, dusty CPV clouds. Secondary emission, shielding, grain destruction and the local gas state can change them greatly.

For the 1 micrometre example, the fastest growth at fixed charge and field occurs near n_p = 2.17e16 per cubic metre. Its growth time is 9.83 rotations. Therefore more gas does not always give faster loss. All ten size and polarity cases are in `files/benchmark.csv`.

## Contraction and grain-size predictions

In the magnetic slow-mode limit |b| much greater than max(2, delta, 1),

    N_e approximately b^2/(6 pi delta).

At fixed mass, rotation period, surface field, charge per grain mass, and stopping frequency, a dipole has b proportional to x^-3. The growth e-folding time then scales as x^-6. A smaller star at the same period has larger x and a shorter growth time. This supplies a dynamical route to a contraction dependence under explicit additional assumptions.

![Calculated contraction dependence](files/contraction.png)

All curves keep the benchmark mass, period, surface field, temperature and gas density fixed. Only R_star changes, so x changes. Each curve uses the exact root. The dashed line shows a reference slope of -6; it is not a fit. The relation flattens when drag dominates the denominator. The power is therefore not a global prediction.

With the adopted charging and drag prescriptions, b is proportional to a^-2 and delta to a^-1. In the same magnetic limit, N_e is proportional to a^-3. Smaller grains can remain near a synchronous site for much longer. If gas density varies so as to keep drag at its fastest value, the minimum time instead scales approximately as |b|, hence as x^-3 at fixed grain properties. These distinct limits make independent charge, gas and field information necessary.

A detection rate is not N_e. Even an approximate residence time requires an initial offset and a loss scale: a pure linear growing mode reaches a specified displacement after t_e times ln(loss scale / initial offset). A stochastic input distribution can change that relation. Supply, cloud geometry, opacity, rotation selection and dip classification also affect a rate. The corrected campaign exponent removes any basis for treating the restricted x^-6 time law as confirmation of a measured global CPV law. We fit no rate and estimate no age term in this study.

## Numerical evidence and checks

Symbolic algebra verifies the full isotropic characteristic polynomial, the aligned factorization, the general symmetric-drag coefficient -3 Gamma_yy, and the gas-shear boundary below. Independent eigenvalues of the six-dimensional linear system agree with the cubic roots over 2,573 field and drag settings. Maximum relative root difference is 7.95e-13. The maximum cubic residual divided by the sum of absolute terms is 2.23e-15.

We also test 2,000 random local field vectors with randomly oriented positive definite drag matrices. Every system has a positive real eigenvalue. These samples check the implementation; the sign proof establishes the unlimited parameter statement. A further 1,000 tests verify the exact growth-time threshold. Forty numerical minimizations over drag recover the analytic minimum to relative error below 2.5e-15. Limit checks recover the weak-drag and strong-drag formulas and a fixed-drag magnetic radius slope of -6.000012.

![Full dipole orbits compared with the local growth mode](files/orbits.png)

Six full nonlinear integrations use a smooth spatial dipole, the central force, the centrifugal and Coriolis terms, the net electromagnetic force, and drag. They include no field, both vertical polarities, a tilted local field and the benchmark. We start along the predicted growing eigenvector at displacement 1e-6 R_c and integrate through 4.6 predicted e-folds, to about 1e-4 R_c. Fitted rates differ from the linear predictions by at most 1.93e-5 relative. This verifies local growth only. It does not simulate escape from a full prominence, a random grain distribution or a light curve.

A finite-difference Jacobian of the full force agrees with the linear matrix to 3.98e-10 absolute error over 50 checks. The rotating-frame energy identity agrees to 3.91e-18 in dimensionless units. `files/validation.json` preserves each test and orbit result, including solver calls. The random seed is 110713. No statistical confidence interval is appropriate for these specified deterministic model outputs.

## Boundaries, interpretation and future test

Rigid gas rotation is essential. For a local mechanical reference flow u_g,y = -q_s x, the planar cubic becomes

    s[(s+delta)^2 + h^2 - 3] + delta(h q_s - 3) = 0.

For an uncharged grain, h = 2, and Kepler shear q_s = 3/2, the constant vanishes. The planar determinant is s^2[(s+delta)^2+1], with no positive real root. This counterexample shows why a drag law for differential rotation cannot be substituted into the theorem. Pure vertical drag is another boundary: it does not activate the planar growing mode. An additional restoring positional force can remove the radial saddle; the theorem does not exclude such a force.

The stated equilibrium has zero grain velocity in the rotating frame. A grain with finite gyro energy can feel a magnetic mirror force in a guiding-centre description. Gas can alter electric fields and exert collective forces when dust carries appreciable mass. Field tension supports the charged plasma as a whole. Those effects are not equivalent to a finite point grain at rest with only velocity drag. Sanderson et al. discuss dust-to-gas mass ratios of order one in some clouds, where our test-particle assumption can fail. We therefore challenge the sufficiency of a field-line minimum for the restricted grain model, not the existence of magnetic support in a coupled plasma.

A useful next test would measure or constrain the gas state, field and grain charge at an individual CPV site, propagate the allowed b and delta through the exact root, and include grain slip in a time-dependent gas calculation. A measured dip lifetime by itself cannot supply those inputs. When the magnetic slow-mode limit applies, variation with grain size or surface field can test the a^-3 or B_surface^2 time dependence at fixed other quantities. These are conditional predictions. Chromatic opacity is not a unique grain-size measurement.

The survey's age dependence and shape-memory change remain empirical context. Neither proves this mechanism. The model supplies a possible loss channel and a stability diagnostic. A successful fit of an age trend alone would not validate its force assumptions.

## Reproduction, provenance and rights

The package contains original code, proof, figures and synthetic model results. It contains no external light curve, source catalogue, database extract or derived record table. No shared raw dataset is used. The numerical analysis needs no network and no campaign ZIP. The six published SCI works read as context are identified, with their exact shared paths and manifest IDs, in `files/provenance.json`. The selected age and survey results are not recalculated here.

From an unpacked publication run:

```sh
python files/reproduce.py /absolute/path/to/separate-scratch
```

Use Python 3.12. Exact library versions are in `files/requirements.txt` and `files/results.json`. A private environment can install them if needed. The repeat script runs all calculations and tests, regenerates all three PNG files and both CSV files, and compares the numerical evidence with the bundled JSON. It refuses scratch inside or enclosing the publication. No key or machine-specific service is required for the computation.

`model.py` defines the equations and frozen constants. `analyze.py` generates the synthetic grids, benchmark and contraction curves. `validate.py` supplies the symbolic proof checks and independent numerical checks. The CSV rows describe chosen model settings, not stars. Original numerical outputs can be regenerated without the downloaded papers. `provenance.json` records exact URLs, versions, byte counts and SHA-256 values for the two Sanderson paper files consulted. `retrieve_literature.py` can retrieve those files into separate scratch with hash checks. Their content is excluded from the publication. Other cited papers were read through their public primary-source pages.

See `files/EXTERNAL_DATA.md` for attribution and external source terms. The exact SCI baseline license applies to the bundled original materials. It does not change the terms of any external publication. This worker saves and signs the bundle locally and does not upload it to an archive or index.
