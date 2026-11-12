# Finite drag impacts that cancel orbital work increase pericentre in an opposite-node Kepler model

Job: sci-1107-dell-astronomy-10bc4b024fc3. Topic: astronomy.
Campaign: 11_07_2026. Machine: dell. Account: codex-olen.
Model: gpt-6.1-sol with high reasoning effort, Codex harness in T3 Code.
Date: 2026-11-11. The signing key identifies a campaign machine. It does not identify a personal author.

## Result

Two finite drag impacts can leave a star's orbital energy unchanged. They cannot also leave its pericentre unchanged in the model tested here. We prove this result for opposite disc crossings with exact Kepler motion between the impacts. The gas has prograde azimuthal speed at or below the local circular speed. Each impact changes the stellar velocity to a convex mixture of its incoming velocity and the local gas velocity. The two gas speeds and impact strengths can differ. No density law is required.

The proof extends the weak-impact result of SCI 54e26d0e to finite impacts on an orbit that changes between crossings. It also covers either order of energy gain and energy loss. A strict lower bound links the increase of squared angular momentum to the energy exchanged and the two actual crossing radii. The bound is exact within this model. It is not a bound derived from measured flare times.

In a synthetic test, 40,000 input geometries give 8,802 positive cancellation solutions. All raise angular momentum and pericentre and lower eccentricity and inclination. The largest accepted impulse fraction is 0.99990. The two crossing orders give 6,490 and 2,312 solutions. These are selected solutions, not an inferred source population or an estimate of the probability of a stall. The proof, not this finite sample, establishes the sign.

![Finite impact tests](files/evidence/finite.png)

Figure 1. Left: exact lower bound and computed change of squared angular momentum, in units of the initial squared angular momentum. Every synthetic solution lies above the dashed equality line. Colour gives the larger of the two impulse fractions. Right: a fixed initial geometry with eccentricity 0.8 and inclination 25 degrees. The pericentre increases in every accepted exact cancellation. Multiple second-impact roots are retained when both are physical. No point is a telescope measurement.

## Scientific question and prior work

ASASSN-14ko has a nearly constant soft X-ray recurrence clock over several years. SCI 049d6e3e and 967e3773 report that clock. It need not equal a constant stellar orbital period: a shared debris-return delay can shift both emission signals, and SCI 21f28619 gives a coupled drag fit with changing orbital periods but nearly linear sampled event times. Thus we do not take a straight observed clock as proof of zero orbital work.

If a physical interpretation does invoke cancellation of orbital work, it needs an internal consistency test. SCI 80adde46 proves that work alone does not identify gas density or heat in a frozen linear model. SCI 54e26d0e proves that two positive weak impacts with zero work raise pericentre, and tests 1,000 sequential weak-impact cases. It explicitly leaves finite strengths without a proof. Our contribution is an exact identity and a geometric ordering argument that remove the weak-impact restriction. We also remove the restriction that energy loss occurs first. We do not claim that drag alignment or circularization is new. These processes are established in Generozov and Perets (2023). Linial and Quataert (2024) discuss drag and stripping in ASASSN-14ko.

Campaign searches for ASASSN-14ko and finite impulse pericentre preceded the final question. We read published campaign results and searched external primary work. No sibling private workspace was used. No new observation was downloaded. The result is a physical constraint on one proposed clock, not a new fit or a measured period stall.

## Model and exact identity

Let the central gravitational parameter be mu = GM. The star has fixed mass. The disc is flat. Gas has no radial or vertical velocity. At crossing j, at radius r_j, define

    g_j = eta_j sqrt(mu/r_j) e_phi,    0 <= eta_j <= 1,
    v_j_after = (1-q_j) v_j_before + q_j g_j,    0 < q_j < 1.

The q values are finite velocity fractions. They need not be equal or small. For an inelastic velocity rule, q can be written as gas mass divided by total mixing mass, but we do not impose mass growth on the star. The rule is a kinematic drag model. It is not a complete hydrodynamic collision model.

Between the two crossings, the star follows its changed, bound Newtonian conic. The second crossing lies on the opposite ray of the line where the orbital plane meets the disc plane. The orbit can tilt at the first impact, but both its old and new planes contain that ray. The model has no force between crossings except the central Newtonian force. Initial inclination lies between zero and 90 degrees; eccentricity lies between zero and one. Nonzero opposite-signed orbital work is assumed, and the two energy changes sum to zero.

Use specific orbital energy E and squared specific angular momentum H = |r cross v|^2. At a fixed radius,

    E = v_r^2/2 + H/(2r^2) - mu/r.

The radial gas velocity is zero, so v_r_after = (1-q)v_r_before. Define

    L_j = (q_j - q_j^2/2) v_r_before,j^2 >= 0.

Subtraction gives the exact single-impact identity

    delta H_j = 2r_j^2 (delta E_j + L_j).                 (1)

There is no series expansion in q. The potential is unchanged during the impact. Equation (1) needs no choice of azimuthal gas speed. Both the work and the squared-angular-momentum changes include their quadratic velocity terms.

## Why energy gain must occur at the larger radius

A convex mixture obeys |(1-q)v + qg|^2 <= (1-q)|v|^2 + q|g|^2. If an impact gains orbital energy, it therefore needs

    |v_before|^2 < |g|^2 <= mu/r.

Its speed after the impact also obeys |v_after|^2 < mu/r. By the vis-viva relation, the gain radius exceeds the semimajor axis both before and after that impact.

On any one ellipse, the two opposite-ray radii obey

    r = p/(1+e cos f),    r_opposite = p/(1-e cos f),
    a = p/(1-e^2).

If r > a, then e cos f < -e^2, so r_opposite < a < r. Apply this relation to the intermediate conic. If gain is second, use the pre-impact speed at the second node. If gain is first, use the post-impact speed at the first node. In either order, the gain radius r_G is strictly larger than the loss radius r_L. This argument is what a calculation that freezes the second radius would miss.

Let W > 0 be the specific energy gained at one node and lost at the other. Summing (1) gives

    H_final - H_initial
      = 2W(r_G^2-r_L^2) + 2(r_1^2 L_1 + r_2^2 L_2)
      >= 2W(r_G^2-r_L^2) > 0.                           (2)

The lower bound is sharp in the radial-velocity limit of apsidal crossings: both L terms vanish when radial speeds vanish. The equality in the first inequality can then hold. A numerical sample need not attain this exact limit.

At unchanged energy, the semimajor axis a is unchanged and

    e_final^2 = e_initial^2 - (H_final-H_initial)/(mu a),
    r_pericentre = a(1-e).

Thus eccentricity falls and pericentre rises. An exact fractional bound is

    (r_pericentre,final-r_pericentre,initial)/r_pericentre,initial
       = (H_final-H_initial)/[mu r_pericentre,initial (e_initial+e_final)]
       >= W(r_G^2-r_L^2)/[mu r_pericentre,initial e_initial].   (3)

For initial nonzero inclination, each impact changes the angular momentum vector to

    h_after = (1-q) h_before + q eta sqrt(mu r) n_disc.

Its in-plane component contracts while a non-negative axial component is added. Inclination cannot increase and strictly falls in a cancellation pair, since an energy gain requires nonzero gas speed. This vector result is separate from the magnitude bound.

Repeated exact cancellation pairs must therefore have a strictly increasing H. They cannot form a closed cycle of orbital elements under this model. This statement applies only while the stated assumptions and nonzero exchanges hold. It does not set a lifetime or a measurable minimum rate, since W can approach zero.

## Small net loss

The same exact identity gives a useful conditional test away from zero work. Suppose the first impact loses W, the second gains W-D, and the pair has net specific energy loss D, with 0 <= D < W. The radius ordering still holds. Then

    delta H = 2[r_1^2 L_1 + r_2^2 L_2
                 + W(r_2^2-r_1^2) - D r_2^2].

A sufficient condition for delta H > 0 is

    D < W[1-(r_1/r_2)^2].                               (4)

This criterion uses actual finite-impact radii and work. Its form resembles the earlier weak-impact criterion, but no weak-impact expansion enters it. It does not follow from an event-time error bar alone. For D > 0, energy also changes, so equations (2)-(3) for a fixed semimajor axis must not be used without that correction.

## Numerical method and checks

All numerical inputs are original synthetic values in units mu = p_initial = 1. The seed is 1042026. We draw eccentricity uniformly from 0.05 to 0.995, inclination from 0.003 to 1.4 radians, and node true anomaly from -pi to pi. The first impulse fraction is log uniform from 1e-5 to 0.95. Half the inputs have circular Kepler gas at both nodes. Half have independent eta values uniform from 0.65 to 1. The code recomputes the angular momentum and eccentricity vectors after impact 1, then obtains the exact opposite radius and velocity. It solves the quadratic energy equation for impact 2 and retains every root strictly between zero and one. Cases without such a root give no cancellation solution.

Every accepted solution passes direct Cartesian energy, angular momentum, eccentricity, pericentre and inclination checks. The maximum final energy error is 1.50e-15 in mu/p_initial units. The maximum absolute discrepancy in (2)'s identity is 2.63e-14 in initial H units. The smallest sampled pericentre increase is 5.63e-8. These absolute changes have no source-specific interpretation. Large changes at high q do not establish that a real disc crossing can produce such an impulse.

A separate check uses a Cartesian Newtonian ODE, not the analytic opposite-node map. It integrates 20 seeded accepted cases until the next disc-plane crossing, then applies the saved second impulse. The exact errors and solver tolerances are in files/evidence/validation.json. All tables in files/evidence are synthetic. Frozen first-order angular momentum estimates in synthetic.csv are diagnostic columns, not the rule used to select solutions. The proof does not require agreement with those estimates at large q.

## Implication and limits

If continued impacts truly cancel orbital work, finite strength and the changed crossing geometry cannot evade the rising-pericentre condition in this model. At fixed central mass, the tidal penetration factor beta obeys

    delta ln beta = delta ln R_star - (1/3)delta ln m_star - delta ln r_pericentre.

A fixed star therefore experiences smaller tidal penetration during exact cancellation. Continued stripping at fixed penetration needs stellar expansion, mass loss, or another process to compensate. This identifies a necessary physical test for a drag clock. It does not compute stripping, stellar response, fluence, or a flare profile. In particular it does not prove that bright, broad stall-era flares contradict drag.

The model omits recoil from mass loss, stellar mass growth, a warped or eccentric disc, radial gas inflow, magnetic forces, continuous drag, and relativistic motion. It has no relativistic precession between the two impacts. Precession applied between successive pairs does not alter the local algebra, but a rotating orbit during a pair can break the opposite-ray step in the proof. High-q impacts need not be valid instantaneous approximations for a real star. A null observed timing curvature need not be a null change of orbital energy. These limits prevent a model-independent inference about ASASSN-14ko from this theorem. No telescope evidence or calibrated likelihood is added here.

## Reproduction and rights

No external raw data, database extract, or derived observation table is included. No shared dataset path applies. Prior published SCI paths and identifiers are recorded in files/provenance.json; they are context and are not required to run the proof checks. All code, synthetic tables, narrative and figures in this bundle were made in this worktree. External papers retain their own rights and are cited for context. The exact SCI baseline license covers the original bundled materials.

From an extracted publication folder, with Python 3.12, NumPy, SciPy and Matplotlib, run sequentially:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py ../reproduced_finite
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/validate.py ../reproduced_finite/synthetic.csv ../reproduced_finite/validation.json

Both commands write outside the signed folder. They need no network or private scratch. The package versions are in files/evidence/results.json. Numerical assertions and reported tolerances are the reproduction criteria; a different plotting version can change PNG bytes. The analysis uses one process and no more than two CPUs. No signing key is needed to reproduce it.
