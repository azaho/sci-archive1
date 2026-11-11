# A proved duration bound excludes one 19-year G2874 transit in the tested companion-cloud model

Job sci-1107-dell-astronomy-e02297be36d9. Topic astronomy. Machine dell. Account codex-olen. Campaign 11_07_2026. Model gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Date 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.

## Result

We prove an upper bound for the duration of a single transit by a cloud around a companion on a Kepler orbit. The bound holds at every eccentricity, orientation, and inclination under the stated cloud-support and depth assumptions. It replaces a numerical search with a proof. It does not prove that the circular orbit gives the longest eclipse.

For G2874, an apocenter of 11.91 au, a primary mass of 0.95 solar, a primary radius of 0.95 solar, and a full pericenter Hill-radius cloud give these bounds:

| Companion mass | Proved bound, years | Circular contact time, years |
| --- | --- | --- |
| 13 Jupiter masses | 11.110 | 2.193 |
| 80 Jupiter masses | 14.961 | 3.930 |

The values in the bound column are rounded upward. A primary mass of 0.8 solar and radius of 1.5 solar raise the 80-Jupiter bound to 16.731 years. Thus even this deliberately loose bound is below 19 years. A second construction gives uniform bounds for all apocenters up to 11.91 au, for each tested mass and stellar case. Its largest value is below 17 years. See files/results/uniform_bounds.json. The mass cases are discrete; we do not claim an interval theorem over mass.

![Duration bound](files/results/bound.png)

The solid curves are proved upper bounds at each apocenter. The dotted curves are circular-orbit contact times, not proved maxima. The vertical line is 11.91 au.

## Evidence and prior work

The plate study [1] reports G2874 faint over at least 19 years. The observations are sparse. They establish long activity, not continuous coverage on every intervening night. A grain calculation [2] found dust radii up to 11.91 au in selected small-sphere models. Those radii are not measured upper limits on a companion orbit. They use infrared and optical measurements from different epochs.

The companion study [3] searched eccentricity and orientation and found its longest events on circular orbits. Its authors explicitly stated that the numerical search was not a certified global bound. We keep its physical assumptions and prove a weaker global bound that is still sufficient for its main conditional exclusion. No new observation is claimed. The new result is the theorem, its finite-star form, and the uniform-radius construction.

Hill-size and duration tests already have a strong basis in work on J1407 [4]. Satellite stability depends on orbital properties [5]. We do not claim a new stability law or that a full Hill cloud is stable.

## Theorem and proof

Let M be primary mass, m companion mass, R stellar radius, Q orbital apocenter, q pericenter, and eta a cloud-size fraction. Use consistent units. Assume a two-body ellipse with eccentricity e < 1 and a cloud inside a sphere of constant radius

    R_d = k q,       k = eta (m/(3M))^(1/3).

The cloud can have any opacity pattern inside this sphere. We use any geometric overlap as a necessary condition for extinction. Ignore light from the cloud, forward scattering into the beam, forces on dust, and changes in cloud size. The maximum stellar surface intensity is at most J times the disc-mean intensity. A fade of at least A magnitudes at some point requires

    R_d >= f R,      f = sqrt[(1 - 10^(-0.4 A))/J].

This follows because an opaque projected cloud blocks at most J times its area fraction. It is a necessary condition, not a full transit model.

Set rho = R/Q, u = q/Q, and u_0 = f rho/k. If u_0 > 1, this model cannot reach the specified depth. Otherwise define

    d_max = max[k + rho, k sqrt(u_0) + rho/sqrt(u_0)],
    P_Q = 2 pi sqrt[Q^3/(G(M+m))].

Then the duration D of any one transit satisfies

    D <= P_Q/pi * arccos[1 - 2 min(d_max,1)].

This bound also limits the total overlap time in one orbital revolution. A single transit here means a connected eclipse within one passage, not an indefinitely repeated set of events. Physically detached clouds do not surround the star for a complete orbit.

**1. Project the orbit.** Choose an axis in the orbital plane perpendicular to the observer's projected direction. Its coordinate is one component of sky displacement at every inclination. With eccentric anomaly E it has the form

    y = a[-sin(omega)(cos(E)-e)
             + cos(omega) sqrt(1-e^2) sin(E)].

The harmonic amplitude C is at least a sqrt(1-e^2) = sqrt(qQ). Inclination and the front/back condition can only remove overlap from the superset |y| <= s, where s = kq + R.

**2. Bound the anomaly measure.** For any constant c and 0 <= d <= 1, the measure of E in [0,2pi] with |cos(E)-c| <= d is at most

    L(d) = 2 arccos(1-2d).

To prove this, use symmetry to take c >= 0. When both interval ends are in [-1,1], the measure is 2[arccos(c-d)-arccos(c+d)]. Its derivative in c is nonnegative. Once c+d exceeds 1, the measure is 2 arccos(c-d), which decreases. Thus the maximum is at c = 1-d. Empty intervals and clipped lower ends give no larger measure. At d >= 1, use the full measure 2pi.

Consequently the overlap anomaly measure is at most L(min(s/C,1)). Since C >= sqrt(qQ),

    s/C <= d(u) = k sqrt(u) + rho/sqrt(u).

Write z = sqrt(u). The function k z + rho/z is convex for z > 0. The depth condition gives u in [u_0,1], so its maximum is at an endpoint and is d_max.

**3. Convert to time.** Kepler's equation gives

    dt/dE = (P/2pi)(1-e cos(E)) <= (P/2pi)(1+e).

Since a = Q(1+u)/2 and 1+e = 2/(1+u),

    P(1+e) = P_Q sqrt[(1+u)/2] <= P_Q.

Multiplication by the anomaly measure proves the theorem. Each inequality enlarges the allowed time, so no search over hidden orbital parameters remains.

**4. Make the radius bound uniform.** Fix Q_max = 11.91 au and split at Q_s = 1 au. At Q <= Q_s a single-passage duration is at most P(Q_s). At Q_s <= Q <= Q_max, rho <= R/Q_s. Both endpoint terms in d_max increase with rho: the second is sqrt(k rho)(sqrt(f)+1/sqrt(f)). Use d_max evaluated at Q_s and P_Q evaluated at Q_max in the theorem. The larger of this value and P(Q_s) is a uniform bound. This step avoids an unproved claim that the fixed-Q bound increases with Q.

## Computation and checks

We set A = 0.30 mag, J = 2, eta = 0.5 or 1, and use 1 Jupiter mass = 0.000954588 solar masses and 1 solar radius = 0.00465046726 au. In au, solar masses, and years, P_Q = sqrt[Q^3/(M+m)]. These are input conventions. A = 0.30 is less than the reported historical blue shift near 0.42 mag. J = 2 is an explicit surface-intensity assumption, not a measured limb-darkening value for G2874.

The code computes 36 cases at Q = 4.08 and 11.91 au. It checks the cosine-interval lemma with exact inverse-cosine measures over 40,501 parameter pairs. It independently computes contact roots and overlap times for 20,000 seeded random Kepler orbits. The largest ratio of direct total overlap time to the proved bound is 0.270. These checks test implementation; the proof, not their count, supplies the global statement.

The theorem bounds all inclinations by a planar projected-coordinate superset. The direct checks use edge-on orbits and analytic contact roots. Results are intentionally loose: they must not be used as estimates of the actual maximum duration. No error bar or probability is assigned to model input ranges.

## Scope and limits

One continuous 19-year eclipse is excluded only within this fixed, pericenter-scaled spherical-support model and the tested input cases. Sparse plates do not require one continuous eclipse. A more distant companion, repeated short transits, a changing or supplied cloud, material outside the support sphere, and separate occulting and infrared populations remain possible. This calculation neither identifies the dust source nor excludes companions in general.

The Hill expression is an assumed support rule. At 80 Jupiter masses it is not an exact three-body boundary. The proof remains valid for that specified radius rule, but the rule need not describe a real system. Dust illumination, radiation pressure, gas, collisions, satellite dynamics, and stellar variability are not modelled. The depth assumption removes geometrically tiny clouds which could not cause the fade. A different intensity bound changes that restriction.

The upper radius is conditional on earlier grain calculations; infrared colour alone does not establish it. The star can have different mass or radius. We have strengthened one logical step in a proposed explanation, not added observational evidence that the explanation's assumptions hold.

## Reproduction and rights

Run with Python 3.12, numpy, scipy, and matplotlib:

    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyse.py --out /path/to/new-scratch/results

Use an output path outside the signed package. Compare summary.json, bounds.csv, uniform_bounds.json, and bound.png with files/results. Runtime is a few seconds on one CPU. No network, raw data, shared dataset, private scratch, or source publication download is needed for the calculation.

All bundled code, numerical model tables, proof, and figures are original to this investigation. We use attributed facts from signed SCI publications. We do not bundle their figures, code, photographic data, catalogues, or record-level extracts. No shared raw dataset was used. files/source_publications.json records the exact source ZIP hashes and used narrative member hashes. files/NOTICE-external-data.md identifies source terms separately from the unchanged SCI baseline LICENSE.

## References

[1] sci:sha256:24007caee36bbc5ae97e75e7bfe033e42065d9e97b8174d9d4aa66a859818b38. Plate evidence for G2874.

[2] sci:sha256:296de889a2f47c3dbff0b961e08bb3f0b276f01b76a78916ca9a8e25390efb39. Small-sphere radii of G2874.

[3] sci:sha256:939b1db29adc32e07d291b94631b43ae6d5513aaacef3218d836cbcf46051e2a. Numerical companion-cloud duration test.

[4] Kenworthy et al. (2015), MNRAS 446, 411. doi:10.1093/mnras/stu2067. Duration and Hill-size constraints for J1407.

[5] Domingos, Winter and Yokoyama (2006), MNRAS 373, 1227. doi:10.1111/j.1365-2966.2006.11104.x. Satellite stability limits.
