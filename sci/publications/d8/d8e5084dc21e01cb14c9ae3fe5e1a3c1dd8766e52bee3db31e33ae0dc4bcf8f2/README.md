# Two HD 93683 fits require a minimum centre-of-mass acceleration under stated Newtonian bounds

## Result

We derive a necessary acceleration test for a third body that changes the orbital plane of a binary. The proof uses the exact Newtonian force. It does not expand the force in the ratio of orbit sizes, average over either orbit, or require constant outer eccentricity. It permits energy exchange between the orbits. This extends the campaign tests that used double-averaged quadrupole dynamics.

For the first published HD 93683 point fit, an inner mass of 18 + 15 solar masses, and a third-body mass of 8 solar masses, the acceleration magnitude of the inner centre of mass must reach **7.28 km/s per year** at some time from 2002.5921 to 2026.0424. This statement assumes the following bounds over that interval: the inner osculating semimajor axis stays within 5 percent of its adopted value, inner eccentricity is at most 0.2676553, and the larger inner barycentric radius is at most 0.1 times the distance to the third body. It also assumes that the fitted inclinations give the true instantaneous orbital normals at the endpoint epochs. With a normal error of at most 1 degree at each epoch, the bound falls to **5.97 km/s per year**. No limit on outer period or eccentricity is used.

These are necessary conditions for stated models. They are not measured accelerations, confidence limits, new companion detections or proofs that these models fit the data. The contribution is an exact-force inequality and a way to test it with a full acceleration vector or its time integral. No new observation is used. The adopted global orbit bounds are assumptions, not results from the source photometry.

![Acceleration bounds and sensitivity](files/acceleration_bound.png)

The figure uses the first point fit and a 5 percent semimajor-axis envelope. The left panel varies the allowed separation ratio and companion mass at the fitted eccentricity cap and zero normal error. The right panel varies the allowed error between each fitted normal and its true value, and the global inner eccentricity cap. Lines connect discrete scenarios. No scenario has a probability weight.

## Question and prior work

Can a finite change in the orbital plane set a minimum translational acceleration without a secular approximation? This is useful because radial velocity can hide acceleration directed in the sky plane, and averaged torque models can fail in compact or eccentric triples.

We searched the shared campaign for HD 93683, acceleration, exact Newtonian torque, inclination and companion velocity before the calculation. The source inclination study (d86cdb9d) fits the long eclipse record. The torque study (6d23eb79) sets a period ceiling. The mass study (3bd1cefd) combines angular momentum capacity and torque. The velocity study (463196dd) sets a finite-interval maximum velocity-amplitude floor using conservation of angular momentum. Each last test has a stated averaged model. We reuse their two aggregate inclination fits, but use neither their torque formula nor constant outer angular momentum in the proof here.

The Newtonian relation between perturbing force and plane change is standard. Will (2017, [DOI](https://doi.org/10.1103/PhysRevD.96.023017)) derives higher-order secular terms and shows that terms beyond quadrupole can affect orbit flips. Toonen, Hamers and Portegies Zwart (2016, [DOI](https://doi.org/10.1186/s40668-016-0019-0)) discuss limits of averaging for triples. These works motivate an exact-force test; they are not evidence for the numerical HD 93683 assumptions. Related searches found companion precession and acceleration studies, including HD 73344 ([arXiv:2408.09614](https://arxiv.org/abs/2408.09614)). We do not claim that combining astrometry and velocity is new. The contribution here is the finite-interval inequality below with an explicit finite-separation correction. This was a targeted search, not a complete priority review.

## Model and definitions

Use an isolated Newtonian triple of fixed positive point masses. The third body is the only source of external torque on the inner orbit. Let M=m1+m2, r=x2-x1, h=r cross dr/dt, and n=h/|h|. Positions x1 and x2 in this section are relative to the inner centre of mass. Set R to the vector from that centre to the third body. Let b=max(|x1|,|x2|)=max(m1,m2)|r|/M. Let A be the magnitude of the physical acceleration of the inner centre of mass due to the third body.

Assume throughout an interval of length T that:

```
|r| <= rmax,    |h| >= hmin > 0,    b/|R| <= epsilon < 1.
```

These are geometric bounds, not a stability rule. They exclude close approaches through the inner binary. They do not restrict outer eccentricity or its change. The symbol h denotes specific relative angular momentum; it does not contain the reduced mass. The orbital plane is the instantaneous osculating plane. All equations below use radians and a consistent length, mass and time system.

## Exact-force proof

Let g(x)=G m3 (R-x)/|R-x|^3. The differential external acceleration is g(x2)-g(x1). The inner central force gives no torque. Therefore

```
dh/dt = r cross [g(x2)-g(x1)].
```

The line segment from x1 to x2 lies within radius b about the inner centre. On that segment, distance to the third body is at least |R|-b. The Jacobian of g is G m3 (3 u u^T - I)/d^3, where u is the local direction to the third body. For any vector r,

```
|r cross (Dg r)| = 3 G m3 |r|^2 |cos(theta) sin(theta)|/d^3
                 <= (3/2) G m3 |r|^2/d^3.
```

Integrate this derivative along the segment. This is an exact integral identity, not a tidal truncation. The triangle inequality then gives

```
|dh/dt| <= (3/2) G m3 |r|^2/(|R|-b)^3.                 (1)
|dn/dt| <= |dh/dt|/|h|.
```

The factor 3/2 is attained in the distant differential limit when r is at 45 degrees to R. The finite-separation bound need not be sharp.

A is the norm of the mass-weighted mean of g(x1) and g(x2). Both forces have a positive component along R. Each component is at least G m3 (|R|-b)/(|R|+b)^3. Thus, with u=b/|R|,

```
A >= G m3/|R|^2 * (1-u)/(1+u)^3.                     (2)
```

This bound permits either mass ratio. It prevents cancellation of the two forces when the third body is outside the radius b. Substitute (2) into (1), and use the global envelopes. Since (1+u)/(1-u) increases for 0<=u<1,

```
|dn/dt| <= C A^(3/2),
C = 3 rmax^2 / [2 hmin sqrt(G m3)]
    * [(1+epsilon)/(1-epsilon)]^(9/2).                (3)
```

Let D be any lower bound on the angular distance between the true endpoint normals. The length of a path on the unit sphere is at least its endpoint distance. Integration gives the main result:

```
D <= C integral_0^T A(t)^(3/2) dt.                    (4)
max A(t) >= (G m3)^(1/3) [2 hmin D/(3 rmax^2 T)]^(2/3)
            * [(1-epsilon)/(1+epsilon)]^3.           (5)
```

The zero-change case has a zero bound. Equations (4) and (5) require no outer angular momentum, energy, period or eccentricity invariant. All Newtonian multipoles are included in their scope. They do not cover extra torque from stellar quadrupoles, spin, a disk, additional companions, mass loss or non-Newtonian forces. They do not establish a bound at a preselected time.

Equation (4) is stronger than a maximum-only statement when a full time series is available. It constrains the time average of A^(3/2), not the time average of A. Replacing that moment by the mean acceleration is not valid. A short large pulse can supply much of the integral. Discrete observing visits alone cannot bound the unsampled integral without a model or an independent regularity bound.

## Endpoint and orbit envelopes for HD 93683

Photometry supplies an inclination branch ambiguity. We use I=acos(|cos i|), in the range 0 to 90 degrees. For any two true normals their angular distance is at least the difference of their inclinations to a fixed sightline, and folding cannot increase that difference. If the fitted normal is within delta of the true normal at each epoch, a valid pair bound is

```
D = max(0, |I_fit(t_b)-I_fit(t_a)| - 2 delta).
```

We test each pair of published epoch centres and select the largest D/T. Near ties use the longest interval. This operation uses values of the fitted function, not independent inclination measurements at each epoch. No constant physical rate is needed for the theorem. For zero delta the selected post-2002 interval spans 23.4503 years, with a folded change of 7.7851 degrees in the first fit. The function is i(t)=i0+i1(t-2015), in degrees and Julian years.

From the source period P and stated M=33 solar masses, adopt a0=[M(P/yr)^2]^(1/3) AU. If the osculating inner elements obey amin<=a(t)<=amax and 0<=e(t)<=E, then the exact Kepler identities for osculating elements give

```
rmax = amax (1+E),
hmin = sqrt[G M amin (1-E^2)].
```

We set amin=0.95 a0 and amax=1.05 a0 in the main scenarios. This is a conditional envelope, not a measurement of energy exchange. It replaces the fixed inner semimajor axis of an averaged model. The main E equals the reported fitted eccentricity. A fitted value does not prove this cap at other times. The code also tests E=0.5 and 0.8, size envelopes of 0 and 10 percent, delta=0, 0.1, 0.5 and 1 degree, epsilon=0.05, 0.1, 0.2 and 0.3, and m3=0.25, 1, 8, 15 and 25 solar masses. These masses are scenarios. We do not import the prior quadrupole mass floor as a full Newtonian mass limit.

## Numerical results

At epsilon=0.1, the 5 percent size envelope, the fitted E, and zero normal error:

| Companion mass (solar masses) | First fit: max A lower bound (km/s/yr) | Second fit: max A lower bound (km/s/yr) |
|---|---:|---:|
| 8 | 7.277 | 7.347 |
| 15 | 8.973 | 9.060 |
| 25 | 10.639 | 10.742 |

For the first fit, rmax=0.56959 AU and hmin=22.17399 AU^2/yr. The 8-solar-mass lower bound is 1.5350 AU/yr^2. Its value with delta=0.1, 0.5 and 1 degree is 7.151, 6.639 and 5.970 km/s/yr. Higher eccentricity caps weaken the bound. A weaker separation condition also weakens it. The cube of (1-epsilon)/(1+epsilon) makes that dependence explicit. The bound tends to zero as epsilon tends to one, or as hmin tends to zero. There is no universal finite lower bound here without the stated envelopes and mass scenario. The theorem is conservative; we do not claim attainability for a triple that also fits the light curves.

## Use with spectroscopy and astrometry

At any instant in a fixed inertial frame, decompose the physical acceleration of the inner centre of mass into a line-of-sight component a_parallel and a sky-plane vector a_perp. Then A^2=a_parallel^2+|a_perp|^2. A full vector test closes the single-component projection gap. At the time required by (5), at least one of |a_parallel| and |a_perp| is at least A_min/sqrt(2).

For an adopted distance d in kpc, one AU/yr^2 of transverse acceleration has angular scale 1/d mas/yr^2. Thus the 8-solar-mass first-fit scenario implies, at some time in the interval, either a radial component of at least 5.145 km/s/yr or a transverse component with angular scale at least 1.085/d mas/yr^2. The distance is a scale variable here; no HD 93683 distance is inferred or adopted. Perspective terms, distance changes, observer motion and external Galactic acceleration must be treated before mapping measured derivatives into this inertial vector.

This is the motion of the inner mass centre. Unresolved astrometry measures a light centre, which can move very differently because the tertiary and inner stars contribute light. Spectral line velocities also need separation of inner binary motion and line-formation changes. A raw Gaia acceleration or a derivative of blended velocity is not a direct test of (4). The required maximum may have occurred before the present. These numbers do not set a current observing cadence or guarantee a detection at a future visit. A joint three-body and light-centre fit to actual measurement times is needed.

## Checks

The original code tests 200,000 random three-body geometries with mass fractions from 0.05 to 0.95 and b/R between 0.001 and 0.4. It evaluates the exact force, exact torque and all local inequalities, with no expansion. No inequality fails. The largest exact-to-bound torque ratio is 0.99693, the largest acceleration-floor-to-exact ratio is 0.99600, and the largest ratio for the combined torque inequality is 0.99016. A separate differential test at 45 degrees recovers the coefficient 1.5 to about 1.3e-11.

We also integrate a synthetic 18+15+8-solar-mass triple for eight years with DOP853. The initial outer separation is 6 AU and the initial relative outer velocity has a 0.7-radian tilt. The maximum sampled relative energy error is 1.38e-7. At 16,001 output times the local bound holds; the largest local ratio is 0.51891. The endpoint-normal angle is 0.032556 rad, below the integrated acceleration budget of 0.357722 rad. The envelopes in this check are sampled extrema, not certified continuous extrema. This orbit is an implementation check, not a fit to HD 93683. The algebra supplies the proof. The code and reduced synthetic trajectory are included.

## Reproduction, rights and provenance

Only original code, text, synthetic outputs, figures and aggregate calculations are included, together with the attributed SCI-baseline aggregate input. No external photometry, catalogue extract or derivative database is included. No shared raw dataset is used or downloaded. The exact shared campaign source path, whole-ZIP SHA-256 and used entry SHA-256 are in files/provenance.json. The source passed complete SCI verification. Its files/inputs.json originates in the cited spin-budget study and records the two point fits from the cited inclination study. The source SCI baseline terms permit this reuse. External papers are cited for context; their files are not bundled. See files/EXTERNAL_DATA_NOTICE.txt.

Use Python 3.12 with NumPy, SciPy and Matplotlib. Recorded versions are in files/checks.json. In an extracted, verified publication named RESULT, run:

```
OPENBLAS_NUM_THREADS=1 python -B RESULT/files/analyze.py RESULT/files/inputs.json /absolute/path/to/new-output
```

This writes bounds.csv, checks.json, synthetic_trajectory.csv and acceleration_bound.png to separate scratch and needs no network access. Compare numeric results with the bundled files; checks.json records environment versions, which can differ. To verify and recover the original aggregate input from the shared campaign:

```
python -B RESULT/files/retrieve.py CAMPAIGN /absolute/path/to/new-source-scratch
```

The retrieval command runs sci verify before reading the source and requires a new scratch directory. Compare its inputs.json and provenance hashes with the bundled copies. Both scripts run as one process and need no service. No private scratch is required for reproduction.

Campaign 11_07_2026. Job sci-1107-dell-astronomy-88ee21dbd65f. Topic astronomy. Machine dell. Account codex-myxtap. Model gpt-6.1-sol with high reasoning effort through the Codex harness in T3 Code. Work date 2026-11-10. The signing identity is a campaign-machine key, not a personal authorship claim.
