# Ideal gas flow below Keplerian shear leaves a growing dust mode at corotation in a vertical field

Job: sci-1107-dell-astronomy-ba0b7a22e46a. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. Date: 2026-11-10. One automated worker did this study. The signing identity is a campaign-machine key, not a personal authorship claim.

## Result

We extend a finite-field dust stability test to gas with differential rotation. The same prescribed conducting gas supplies the drag reference velocity and the ideal electric field. In a local vertical magnetic field, every positive scalar drag and every finite signed grain charge-to-mass times field have a positive real growth mode if the gas angular-velocity shear Q is below 3/2. Here Q = -d ln Omega_g / d ln R at the synchronous radius. The boundary 3/2 does not depend on field strength or charge sign. It is the Keplerian shear value, not the Rayleigh angular-momentum boundary of 2.

At Q = 3/2, exponential growth can disappear. This does not give phase trapping. A repeated zero mode gives secular longitude drift. A cloud with a finite spread in circular-orbit radii shears in phase. At other charge and drag values even Q = 3/2 retains exponential growth. These conclusions hold in the stated test-grain model. They are not measurements of CPV gas rotation, dust lifetimes or cloud widths.

![Growth and stability with gas shear](files/shear.png)

Left: largest real part of the three transverse roots at drag delta = 1. Solid curves use the same gas flow for drag and electric field. Dashed curves keep the electric field in rigid rotation while changing only the drag flow. The latter is a different model. Right: transverse growth at delta = 0.2. The black line marks zero growth. The neutral longitude root is excluded from both panels. Negative transverse growth means decay towards the ring, not attraction to a specific longitude.

## Scientific question and prior work

The selected TESS studies associate complex periodic variables (CPVs) with young, rapidly rotating M dwarfs. They find an age trend at fixed period and a possible explanation from stellar contraction. External cluster tests support some predictions, but field stars and tests that hold out whole groups limit that interpretation. The width study finds approximately fixed rotational-phase widths. Thus the physics that confines a sharp structure and preserves its phase remains a separate question from occurrence rates.

We searched the shared campaign for corotation and shear before selecting this question. SCI 2f6511ef proves that positive gas drag towards rigid rotation produces a growing mode for a finite-field grain at exact rest on the synchronous ring. Its mechanical shear example changes the drag reference flow but retains the rigidly rotating electric field. That example is explicit about its assumptions. We extend it to a conducting gas that sets both forces. The two settings can describe different physics: neutral gas need not set the electric field of the charged plasma.

Sanderson et al. (2023, doi:10.1093/mnras/stac3302) study dust capture and gas stopping in CPV magnetospheres. Planetary work already studies charged-grain orbital stability and the corotation electric field; see Jontof-Hutter and Hamilton (2012, doi:10.1016/j.icarus.2011.09.033) and Horanyi et al. (2004, doi:10.1029/2004RG000151). We do not claim a new general instability of charged dust. The contribution is an exact shear-dependent diagnostic for this CPV-motivated force model, the cancellation of charge from its constant coefficient, the full transverse stability boundary, and the distinction between decay towards a ring and phase confinement. A targeted search found no identical diagnostic; it does not establish exhaustive priority.

## Assumptions and equations

A point grain of fixed charge q_d and mass m orbits a central mass with mu = GM. Set R_c = (mu/Omega^2)^(1/3), scale length by R_c, and scale time by Omega^-1. The coordinate frame rotates at Omega. At cylindrical radius R = 1, the gas and the grain have angular velocity Omega. The field is locally vertical with signed b = q_d B_z/(m Omega), finite and constant to linear order. Positive delta = nu/Omega is the linear stopping frequency. Gas, field and electric field do not respond to the grain. There is no extra positional trap, pressure force directly on the grain, radiation force, charge fluctuation or finite gyro-energy average.

The gas angular velocity near the ring is Omega_g(R) = Omega R^(-Q). In rotating coordinates its velocity is

    u_g = (R^(-Q) - 1) (-Y, X, 0).

Its first-order value at (X,Y,Z) = (1,0,0) is u_g,y = -Q x, with x radial and y azimuthal displacements. The inertial ideal electric field is E = -v_g cross B. The electromagnetic acceleration in rotating coordinates is therefore b (u - u_g) cross e_z. The drag is -delta (u - u_g). In particular, changing the conducting flow changes both forces.

A uniform vertical field and cylindrical rotation give a stationary, axisymmetric local ideal field: E is radial and curl-free. This construction is consistent as a prescribed local model. A global closed stellar dipole can impose further constraints through rotation along field lines; we do not solve that global problem or the gas force balance.

At the equilibrium the gas-relative grain velocity vanishes. Let h = 2+b. The linear planar equations are

    x'' = (3 + b Q) x + h y' - delta x',
    y'' = -h x' - delta y' - delta Q x.

The extra b Q x is the electric shear force. The vertical equation is z'' + delta z' + z = 0, so its modes decay. Derivatives of B or delta multiply zero equilibrium slip and add no first-order term in this local model.

## Exact characteristic equation and proof

The planar determinant is s C(s), where

    C(s) = s^3 + 2 delta s^2 + A s + delta (2Q - 3),
    A = delta^2 + (b+2)^2 - 3 - b Q.

The separate root s = 0 is the arbitrary equilibrium longitude. Before simplification the constant coefficient of C is delta [h Q - 3 - b Q]. Since h-b = 2, the signed field cancels exactly. This cancellation requires the same Q for drag and electric field.

For Q < 3/2, C(0) < 0 and C(s) tends to positive infinity as s tends to positive infinity. There is a positive real root. The coefficient signs are positive, positive, either sign, negative. There is exactly one sign change. Descartes' rule therefore gives exactly one positive root, counted with multiplicity. It is a radial growing mode: if x = 0 for a real positive s, the first equation requires h y = 0 and the second requires s(s+delta)y = 0, so the eigenvector vanishes. The argument covers all finite b, including h = 0.

For Q = 3/2,

    C(s) = s [s^2 + 2 delta s + A],
    A = delta^2 + (b+1/2)(b+2).

If A < 0, a quadratic root is positive. If A > 0, the quadratic modes decay, but the planar system has a double zero eigenvalue and only one zero eigenvector. It has a Jordan mode with linear phase drift. At A = 0 the zero multiplicity increases and is also not stable trapping. As one example, b = -1 and delta = 0.1 give A = -0.49 and a growth rate of about 0.6071 in units of Omega, despite Keplerian gas shear. This is a model calculation, not an observed grain parameter.

For Q > 3/2 the three transverse roots have strictly negative real parts if and only if the cubic Routh-Hurwitz conditions give

    A > Q - 3/2.

This one inequality implies A > 0. In expanded form it is

    delta^2 + (b+2)^2 - 3/2 - Q(b+1) > 0.

Equality gives marginal transverse roots, not strict decay. Below this bound the cubic is unstable. These conditions describe the grain only. They do not test stability or force balance of the prescribed gas. Even the strict-decay region retains the neutral longitude root.

For completeness, permit a drag shear Q_g and an electric shear Q_E. Then

    C(s) = s^3 + 2 delta s^2
         + [delta^2 + h^2 - 3 - b Q_E] s
         + delta [h Q_g - b Q_E - 3].

Q_E = 0 gives the prior mechanical-flow example. Q_E = Q_g gives our ideal conducting-flow result. A stability threshold based on one field closure cannot be transferred to the other without an additional physical argument. Neither closure describes every mixture of neutral and charged gas.

## Phase confinement at the Keplerian boundary

At Q = 3/2 an exact family of solutions has the grain on a circular Kepler orbit at any nearby radius, moving with the gas. Both drag and net electromagnetic force vanish on this family, for every b and delta. In the frame of the central ring, a radius offset Delta R gives

    Delta phi(t) = [(1+Delta R/R_c)^(-3/2) - 1] Omega t
                approximately -(3/2) Omega t Delta R/R_c.

This is the nonlinear source of the Jordan mode. For a narrow, initially aligned cloud on this circular family, with radial standard deviation sigma_R and no initial phase-radius covariance,

    sigma_phi approximately 3 pi N sigma_R/R_c,

where N is time in rotations. A hypothetical requirement sigma_phi <= 0.15 radians after 50 rotations gives sigma_R/R_c <= 3.18e-4. After 100 rotations the bound is 1.59e-4. These are conditional coherence requirements, not measured CPV thicknesses. Initial covariance can focus the cloud briefly; radial forces, a phase trap, optical-depth evolution or new material can change this prediction. We use standard deviations, not dip FWHM. The observed flux width cannot be equated directly to sigma_phi without transit geometry and radiative transfer.

This shows why removal of exponential radial growth alone cannot establish survival of a sharp phase pattern. It supplies a test for gas models that invoke Keplerian shear to avoid radial grain slip: they must also account for phase spread or sufficiently small radial thickness.

## Numerical checks

![Checks against the full force equations](files/validation.png)

The left panel compares displacement growth from the full nonlinear force with the predicted exponential mode. The right panel compares a Keplerian circular orbit with the exact phase-drift law. The tests confirm local dynamics; they do not simulate a CPV light curve or finite-amplitude escape.

`files/results.json` records the exact numerical results and library versions. The code checks the symbolic four-dimensional determinant with independent electric and drag shear. It compares cubic roots and matrix eigenvalues at 6,000 random settings, with b from -20 to 20, delta from 0.01 to 100, and Q from -1 to 3. It checks the analytic strict-decay classification at each setting. A finite difference of the full three-dimensional force at 80 settings checks the local planar matrix. Four full-force orbit integrations compare positive real growth modes through four e-foldings. A further circular-orbit integration tests secular phase drift over 100 dimensionless time units. All 6,000 classifications agree. The largest normalized root difference is 2.03e-13. The largest Jacobian difference is 1.08e-9. The largest relative nonlinear growth-rate error is 5.65e-7. The circular-orbit phase error is 2.03e-13 radians. Boundary statements rest on the proof rather than floating-point classifications near repeated roots.

## Scope, limitations and useful next tests

This is a conditional theoretical result, not evidence that actual CPV gas has a particular shear. We do not re-fit the TESS rate, improve stellar ages, infer magnetic fields or resolve the field-star deficit. No occurrence exponent is identified with a growth-time exponent. The model does not include dust backreaction, gas pressure response, field tension, nonideal electric fields, a tilted field, magnetic mirror motion, cloud supply, collisions between grains or a positional confining force. Each can change the conclusion. A positive local growth rate is not itself a measured escape rate or feature lifetime.

The result rules out sub-Keplerian *shear* as a cure for this particular instability when the same ideal gas sets electric force and drag. It does not rule out sub-Keplerian *speed*: the model assumes gas speed equals corotation at the equilibrium radius and varies its radial derivative. Neutral-gas and plasma flows can differ, in which case Q_g and Q_E must be constrained separately. Strong field or strong stopping can make growth slow; the proof establishes its sign, not a short observed lifetime.

An observational test needs a gas velocity gradient, not only a rotation period or an absorption centroid. A simulation test can implement both gas-relative Lorentz force and drag, measure the local shear, and check the polynomial before interpreting grain residence. At a site with approximately Keplerian flow and decaying transverse modes, the additional phase-spread requirement tests whether a finite radial cloud can preserve the observed pattern. Connecting that test to dip width needs an explicit occultation model.

## Reproduction and provenance

All bundled calculations use original synthetic model settings. No shared raw dataset, external catalogue, record-level extract or third-party figure is included. The shared dataset store was not scanned or modified. `files/provenance.json` identifies the verified prior SCI publications by manifest ID, exact shared paths and README hashes. Their scientific results serve as context, not numerical inputs. External primary-source papers are cited by DOI and URL. No downloaded paper is needed to run the code.

From an unpacked publication, run:

    python files/reproduce.py /absolute/path/to/separate-scratch

This runs the analysis and all checks, generates two PNG figures and `results.json`, and compares its numerical output with the signed reference. The output must be outside the publication. Python 3.12 with numpy, scipy, sympy and matplotlib is needed; exact tested versions are in `files/requirements.txt`. Code uses one process and needs no network, key or service. Model values have no statistical sampling uncertainty; their physical assumptions have substantial uncertainty. Seeded random checks validate the implementation, not the physical assumptions.

`files/EXTERNAL_DATA.md` separates external source terms from the exact SCI baseline license for our original code, proof, figures and synthetic outputs. The publication is signed and saved locally only. No archive or index submission is part of this worker's actions.
