# A secular evection model permits large tidal-depth changes for two ASASSN-14ko companion fits

Job: sci-1107-dell-astronomy-38af33aec3fe. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. Date: 2026-11-11. The signature identifies a campaign machine. It is not a personal authorship claim.

## Question and result

Can relativistic precession protect a repeating tidal encounter from a close companion? Not in all cases. A companion can act in resonance with the precession. We map this effect for the two circular companion fits proposed for ASASSN-14ko. The calculation averages over the stellar orbit, but retains the companion phase. It assumes a massless star, a circular outer orbit, prograde motion in one plane, a quadrupole tide and leading Schwarzschild precession. It is a conditional theory result. It is not a new timing measurement, a companion detection or a fit of the observed stall.

At an active black-hole mass of 10 million solar masses, the two fits have stable resonance centres at stellar eccentricity 0.96852 and 0.93319. Their formal resonance domains overlap the nominal eccentricity 0.9 used in the earlier orbit study, for some apsidal phases. In a 19-year test at initial eccentricity 0.9 and relative apsidal angle pi/2, the long-period model changes pericentre by a factor of 2.228. The short-period model reaches a 20-gravitational-radius model boundary in 3.221 observer years. Its later path is not predicted here.

The new contribution is a resonance map, a stellar-radius scale and a diagnostic for which outer-phase averaging fails. The result gives a physical interpretation that can be tested in a joint orbit and flare model. It does not show that ASASSN-14ko occupies the resonance.

## Prior evidence and scope

The assignment describes a constant soft-X-ray recurrence near 108.44 days during part of the observing span. SCI 049d6e3e gives that reference clock. SCI e6845f16 separates added precursor and late emission from a main optical event. These findings constrain the measured emission clock; they do not identify a stellar pericentre without an additional physical model.

SCI 4a95f451 found two circular light-time fits with intrinsic decay. SCI 5c61605c then integrated companion gravity and showed changes in passage times and tidal depths, with and without central precession. That work already establishes the missing dynamical term. We do not claim its result as new. We instead calculate the resonance structure behind one possible strong response. We do not assume that every orbit in that earlier study is resonant.

Evection is an established resonance between apsidal precession and outer orbital motion. Frouard et al. (2010), doi:10.1051/0004-6361/200913048, discuss its Hamiltonian structure. Munoz et al. (2022), arXiv:2204.06002v1, apply relativistic evection to a different system: a compact binary orbiting a massive black hole. We apply the same physical principle to a stellar orbit around the flaring hole in the two proposed ASASSN-14ko companion fits. A campaign search for ASASSN-14ko and evection returned no results. We make no claim that evection itself is new.

## Inputs and units

We use the iterative circular fits reported in SCI 5c61605c: observer outer periods 2159.1445 and 4488.6958 days and mass functions 3.41905 and 9.53695 million solar masses. These differ slightly from the scan results in the earlier summary. The stellar reference period is 108.44 observer days. Redshift is 0.0425. Edge-on outer motion sets the minimum companion mass at each active-hole mass. No raw data are downloaded. No shared dataset path is required. Exact source ZIP paths and SHA-256 hashes are in files/provenance.json.

Set G M1 = a = n_inner = 1. Write j = sqrt(1-e^2), delta = varpi - lambda_outer, nu = P_inner/P_outer and q = M2/M1. The circular separation is R = [(1+q)/nu^2]^(1/3). Define epsilon = q/R^3 = q nu^2/(1+q) and gamma = G M1/(a c^2). Both periods used in ratios are in the same frame. Multiplying dimensionless time by 108.44/(2 pi) gives observer days.

For M1 = 1e7 solar masses, a = 93.256 AU, gamma = 0.00105847, and q = 1.17318 or 2.08675. The outer orbit is prescribed. The star cannot change it.

## Derivation

The companion tide in the frame of the active hole has potential

    Phi = (epsilon/2) [r^2 - 3(r dot Rhat)^2].

A mean-anomaly average gives <r^2> = 1 + 3 e^2/2 and <(r dot Rhat)^2> = 1/2 + 3 e^2/4 + 5 e^2 cos(2 delta)/4. The rotating Hamiltonian, with irrelevant constants retained for checking, is

    H(j,delta) = -3 gamma/j
                 - epsilon/4 [1 + (3/2)(1-j^2) + (15/2)(1-j^2) cos(2 delta)]
                 - nu j.

This expression is not expanded in eccentricity. It is truncated in a/R and in relativistic order. Hamilton's equations are

    dj/dt = -(15/4) epsilon (1-j^2) sin(2 delta),
    ddelta/dt = 3 gamma/j^2 + (3/4) epsilon j [1+5 cos(2 delta)] - nu.

The stable centre is at delta = pi/2. It obeys 3 gamma/j_c^2 - 3 epsilon j_c = nu. The saddle is at delta = 0 and obeys 3 gamma/j_s^2 + (9/2) epsilon j_s = nu. The Hessian products have positive and negative signs, respectively. The level H(j_s,0) defines the separatrix, which separates oscillation of delta from circulation. We solve its two roots on the delta = pi/2 cut. The map covers 181 masses from 1e5 to 1e8 solar masses for each outer fit. These are design points, not samples from a population.

If one also averages over the outer phase, the cosine term vanishes and dj/dt = 0 in this planar model. That procedure removes the resonance and every eccentricity change calculated here. It cannot be used to test this effect. The small-amplitude oscillation period is 108.44/sqrt(H_jj H_delta_delta) observer days at the stable centre.

## Quantitative results

| Outer fit | Centre e | Formal e range on the widest island cut | Small-amplitude period, observer yr | Centre pericentre / gravitational radius |
| --- | ---: | ---: | ---: | ---: |
| Short | 0.96852 | 0.89170-0.99065 | 4.704 | 29.74 |
| Long | 0.93319 | 0.85186-0.96919 | 15.744 | 63.12 |

These values use M1 = 1e7 solar masses. The island range is a formal Hamiltonian result. Its highest-eccentricity part can enter a region where the leading precession model is not accurate. It is not a range of measured stellar eccentricity. A value inside the widest cut is not resonant at every delta.

![Resonance map](files/results/resonance.png)

Figure 1. The curves show stable centres. The bands show the formal extrema on the delta = pi/2 separatrix cut. The dashed line marks a pericentre of 20 gravitational radii; values above it enter the excluded region for the trajectory tests. The right panel shows formal separatrices at 1e7 solar masses. They are conditional model boundaries, not observational confidence regions.

We start six secular tracks at e = 0.9, with delta = 0, pi/4 or pi/2, and run for 64 reference periods (19.001 observer years). We stop at pericentre 20 gravitational radii. This is a chosen validity cut, not a tidal-disruption or capture boundary.

| Outer fit | Initial angle | Full span reached | Max/min pericentre | Elapsed observer yr |
| --- | --- | --- | ---: | ---: |
| Short | 0 | Yes | 1.599 | 19.001 |
| Short | pi/4 | Yes | 1.914 | 19.001 |
| Short | pi/2 | No | 4.724 before cut | 3.221 |
| Long | 0 | Yes | 1.596 | 19.001 |
| Long | pi/4 | Yes | 3.815 | 19.001 |
| Long | pi/2 | Yes | 2.228 | 19.001 |

![Domain-limited tracks](files/results/tracks.png)

Figure 2. Model pericentre and relative apsidal angle. The short solid track stops at the validity cut. All tracks have fixed secular semimajor axis. These are not reconstructed observed orbits. The long pi/2 case has bounded angle in this interval; the short pi/2 case is incomplete, so its full oscillation is not established by the track.

## A stellar scale from the resonance

Neglect the small axisymmetric tide in the centre equation. Then j_c^2 is approximately 3 gamma/nu. At high eccentricity, 1-e is approximately j^2/2. Thus

    r_pericentre / r_g is approximately 3/(2 nu).

The period ratio fixes this leading resonance scale almost independently of active mass. The exact centre is at 29.74 or 63.12 gravitational radii at 1e7 solar masses. For a one-solar-mass star with penetration factor beta = r_t/r_pericentre = 1, the tidal-radius equation gives stellar radii 2.93 or 6.22 solar radii. At M1 = 7.1e7 solar masses the exact centre needs 11.31 or 25.66 solar radii. For other stellar masses the required radius scales as M_star^(1/3), at fixed beta; for other beta it scales linearly with beta. These are model scales, not inferred star properties. They give a test: a star far from the required density cannot have both beta near one and sit at that resonance centre.

## Checks and limits

The code checks the averaged potential by independent Cartesian eccentric-anomaly quadrature at four eccentricity and angle pairs for each fit. Errors are below 1e-12 in the dimensionless potential. An independent Cartesian torque average checks dj/dt, including its sign and factor. Finite differences check the stationary points. Hessian signs check their stability. DOP853 uses relative tolerance 1e-11 and absolute tolerance 1e-13. All checks passed. Saved model tracks and parameters permit direct inspection. These checks establish the implemented secular model. They do not validate its approximation against full relativistic three-body dynamics.

The hierarchy is finite. Higher multipoles, variation during one inner orbit, mixed relativistic terms, spin, disc forces, stripping and stellar structure can move the boundaries. At 20 gravitational radii the weak-field expansion parameter is already 0.05. The cut is conservative bookkeeping, not proof of accuracy outside it. We do not replace the more complete orbit integrations of SCI 5c61605c with this secular model. Their initial radial-period calibration and this model's fixed Kepler action are also different.

Only coplanar prograde motion is included. The companion fits and edge-on mass functions are conditional. We do not calculate capture probability, migration into resonance, long-term survival, observed passage times, flare luminosity or spectral line shifts. The fixed-semimajor-axis model does not establish a stalled orbital period or explain the measured episodes. It supplies an additional physical mechanism that a joint fit must test. In particular, precession cannot be assumed to suppress companion torques merely because the orbit remains within a Roche size scale.

## Reproduction and files

The bundle contains original code, model tables and figures under the exact SCI baseline license. There are no external raw data or derived record databases. Source attribution and terms are in files/NOTICE.md. The only numerical external inputs are the cited aggregate fits, listed above and hard-coded in resonance.py. No private scratch is needed.

Use Python 3.12 and files/requirements.txt. From outside the signed directory run:

    bash /path/to/publication/files/reproduce.sh /path/to/new-output

The script writes only to the requested output and uses one numerical thread. resonance.py creates the map, fixed points and derivative checks. validate.py creates the domain-limited tracks, stellar scales, independent average checks and version record. The results are deterministic. The complete calculation takes less than a minute on this host. Compare the CSV files to files/results/. The source SCI ZIPs can be checked with sci verify at the paths in provenance.json, but they are not required to run the model.

An independent rerun reproduced all 16 saved result files byte for byte. The per-file comparison is in files/reproduction_check.json.
