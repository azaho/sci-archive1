# A finite-depth annular screen keeps a sharp direct X-ray ingress for 14 cycles despite Kepler shear

Job sci-1107-dell-astronomy-c8c674bf5252. Topic astronomy. Campaign 11_07_2026. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Date 2026-11-11. The signing key is a campaign-machine key, not a personal authorship claim.

## Result

Kepler shear does not by itself require a broad X-ray ingress from an extended opaque screen. We test one finite-depth circular annular sector, with no reset and no force that prevents azimuthal shear. Radial layers absorb the same ray in series. Their extinction depths add before one computes the transmitted flux. They must not be treated as separate source images whose fluxes add.

For an annulus with radial width 1 percent of its inner radius, a radial grey extinction depth of 1,000, and an inner orbital period of 108.44 observer days, the direct flux falls from 80 to 5 percent in 1.50-1.51 days in all cycles 1-14. Its half-flux time moves only 0.022 days relative to the inner-edge phase between cycles 1 and 14. Its intervals below five percent grow from 34.15 to 55.30 days. There is no change of the orbital period. The late edge, rather than the sharp early edge, records most of the shear.

This is an existence result for direct-beam transfer in a prescribed geometry. It is not a fit to the observed X-ray dips, a gas survival model, or evidence that obscuration explains ASASSN-14ko. The reference sector needs about six solar masses when its grey mass opacity is 0.34 cm2/g. No claim is made that this much opaque gas can have the required geometry. The result gives a specific duration test and identifies a limit of an ingress-only shear test.

![Synthetic direct transmission and duration](files/screen.png)

The left panel compares three synthetic ingresses with a rigid opaque edge. The middle panel shows the growing intervals below five percent. The right panel shows how finite depth changes the ingress. These are model curves, not telescope measurements.

## Why this test matters

The original timing work found a constant soft X-ray dip period near 108.44 days. The 2023 dip was grey and had a fast ingress. A later screen fit showed that a straight opaque edge across a steady Gaussian source can fit that ingress. It needed an extended strip to explain the long low state (SCI a820d6c7). A star-confined screen fails a separate duration bound (SCI 1d967481). An ionized scattering screen has separate radial ionization limits (SCI c1cbdfed). None of these results proves that detached gas can survive shear.

We searched the campaign for ASASSN-14ko and for shear before choosing this test. We found no published campaign calculation of serial, finite-depth transfer through a sheared annular sector. This work extends the opaque-strip test to one evolving sector. It does not claim that orbital shear, cloud eclipses, or opacity saturation are new ideas. Prior AGN eclipse work uses Kepler motion to connect duration to source and cloud scales (Torricelli-Ciamponi et al., MNRAS 442, 2116; doi:10.1093/mnras/stu969). Baskin, Laor and Stern discuss shear in pressure-confined gas (doi:10.1093/mnras/stt2230).

The central physical question is which edge sets the clock. In the tested model the fastest layer sets ingress; slow outer layers extend egress. Thus a stable ingress can time one edge of a gas pattern, without measuring the orbit of the surviving star. The later Einstein Probe result also shows that a fixed optical lag is unsafe after 2024 (SCI 967e3773). This publication does not assume that the optical evidence for renewed orbital decay is established.

## Model and exact transfer equation

Let the inner radius be a, and use r in units of a. The screen occupies 1 <= r <= 1+epsilon, with epsilon = 0.01. Its angular interval at formation is [-alpha,0]. Each radius moves on its own circular orbit:

    Omega(r) = (2 pi / P) r^(-3/2)
    theta_low = Omega(r) t - alpha
    theta_high = Omega(r) t
    alpha = 2 pi (34 d) / P
    P = 108.44 observer days.

This is a prescribed test screen, not stellar debris derived from a disruption simulation. It is viewed in its orbital plane. It has constant volume extinction coefficient inside the sector, so that the full radial depth is tau. It has no radial motion. Gas self-gravity, pressure forces, viscosity, radiation forces, and relativistic corrections are omitted. Mass and volume remain constant under the specified azimuthal advection.

The observer is on the positive x axis. Parallel rays have source coordinate y. A ray intersects a front radial shell at angle asin(y/r). In cycle n define

    h(r,y,t) = Omega(r) t - asin(y/r) - 2 pi n.

The ray crosses the sector where 0 <= h <= alpha. For the cycles and time windows in this test, h decreases with radius and no other angular wrap intersects the ray. Bisection finds the endpoints r_l and r_h of this radial interval. Clipped roots give zero or full coverage where appropriate. The path length, with all distances in units of a, is

    ell(y,t) = max[0, sqrt(r_h^2-y^2) - sqrt(r_l^2-y^2)].

This uses dx/dr = r/sqrt(r^2-y^2). The normalized direct flux is

    F(t) = integral g(y) exp[-tau ell(y,t)/epsilon] dy,
    g(y) = exp[-y^2/(2 sigma^2)] / [sqrt(2 pi) sigma].

We use sigma/a = 2 pi w/P = 0.034956, where w = 0.6033 observer days is the rounded conditional Gaussian crossing scale from SCI a820d6c7. This chooses a source size; it does not estimate a new source size. The Gaussian integral extends to seven sigma. Vertical height is treated as infinite for transfer. A finite half-height of four sigma leaves an uncovered Gaussian fraction of 0.0000633 and is used only for the reference mass. The neglected vertical flux is much smaller than the five-percent threshold. Relativistic image transfer and finite line-of-sight source depth are not included.

All quoted timing values use observer days. To compute the physical reference radius we use a source-frame period P/(1+z), z=0.0425, and black-hole mass 10^7.86 solar masses. These are reference choices, not a new mass measurement.

## Why a sharp edge can survive large shear

For a point ray at y=0 just after the fastest boundary crosses the line of sight in cycle n, let d be time after nP. Before the slower layers catch up, the covered radial fraction is exactly

    f_r = { [1 + d/(nP)]^(2/3) - 1 } / epsilon.

The depth reaches one when

    d_1 = nP { [1 + epsilon/tau]^(3/2) - 1 }
        = (3/2) nP epsilon/tau + higher order terms.

At cycle 14, epsilon=0.01 and tau=1,000 give d_1=0.02277246 d. The full orbital-phase spread is about 23 d, but only a small radial column is needed to remove the direct beam. A Gaussian source then sets most of the observed 1.50-d ingress width. As tau grows, the direct ingress approaches the edge at the inner radius; shear does not impose a depth-independent lower width.

This is not the variance of a sum of layer light curves. Averaging layer fluxes would describe separate source images or disjoint rays. It does not describe this line-of-sight geometry.

In the opaque point-source limit, the first blocking layer has period P. The last clearing layer has period P_out = P(1+epsilon)^(3/2). The interval grows each cycle by

    Delta T = P_out - P = 1.63066 d for epsilon=0.01.

Finite source size and depth alter the threshold times but retain this duration trend at high depth. The constant-period early edge and drifting late edge are therefore linked predictions. For small epsilon, a measured upper bound D on duration growth per cycle would constrain epsilon approximately below 2D/(3P), within this model.

## Numerical results and checks

| Radial depth | Cycle | 80 to 5 percent ingress (d) | Half-flux offset (d) | Span below five percent (d) |
|---|---:|---:|---:|---:|
| 10 | 14 | 6.415 | 1.657 | 43.36 |
| 30 | 14 | 2.533 | 0.643 | 52.26 |
| 100 | 14 | 1.615 | 0.220 | 54.72 |
| 300 | 14 | 1.513 | 0.075 | 55.18 |
| 1,000 | 1 | 1.500 | 0.001 | 34.15 |
| 1,000 | 7 | 1.501 | 0.012 | 43.91 |
| 1,000 | 14 | 1.502 | 0.022 | 55.30 |

The high-depth model was checked in every cycle 1-14. The source grid has 601 points. Changing it to 301 and 1,201 changes the three cycle-14 ingress thresholds by less than 0.0012 d. A separate dense radial integration checks four fluxes at depth 10. It does not use bisection or the analytic path endpoints. The exact point-ray depth-one delay and its small-width expansion agree to 0.00000006 d. Full checks and unrounded values are in files/results.json and files/validation.json.

The input w is a conditional fit with tested noise dependence, not a confidence bound. Our model width of 1.50 d is about 1.44 source-frame days at z=0.0425. Its proximity to the published 1.4-d ingress is a scale comparison, not a statistical goodness-of-fit test. There is only one resolved ingress in the cited XMM campaign. We do not infer a sharp ingress in every observed cycle.

## Physical costs and limits

At the reference mass the inner radius is 2.6994 x 10^15 cm, or 252.34 gravitational radii. The Gaussian size is 9.4362 x 10^13 cm. With half-height H=4 sigma and grey opacity kappa=0.34 cm2/g, the sector mass is

    M_screen = alpha H a (2+epsilon) tau / kappa.

At tau=1,000 this is 5.97 solar masses, with radial mass column 2,941 g/cm2. At tau=100 the mass is 0.597 solar masses and the cycle-14 ingress is 1.615 d. Mass scales as tau times M_BH^(2/3) for the fixed dimensionless geometry and period. These are material costs of this family, not measured gas masses or universal lower bounds. Smaller vertical height, a different projected brightness distribution or nonuniform density changes them.

A Thomson extinction coefficient is only a reference mass conversion. We compute the unscattered direct beam. Scattered or reflected photons can refill the dip and change the spectrum. A high scattering depth is not by itself a sufficient condition for a dark total flux. Ionization, true absorption, energy dependence, re-emission, time delays and viewing angle require radiation transfer. The radial ionization bound in SCI c1cbdfed applies separately to directly illuminated ionized gas; this calculation does not evade it.

The required vertical extent, abrupt boundaries and constant density are prescribed. We have not shown hydrostatic balance, thermal stability, magnetic confinement, supply from a star, or survival against evaporation and radiation. A cold cloud and an ionized scattering screen each have further problems. The sector cannot remain a transient eclipse forever: eventual azimuthal wrapping removes its uncovered phase. No fit to the historical dip durations is attempted. Continuous low intervals in the model must not be confused with proof of continuous low flux between sparse observed visits.

The calculation establishes a kinematic and direct-transfer counterexample to a depth-independent shear-width exclusion. It does not establish an AGN obscuration mechanism or explain the stalled period change. Its main empirical consequence is to seek an egress drift, rather than infer radial thickness from ingress sharpness alone. A regenerated screen, noncircular trajectories or density changes can evade the duration prediction but lie outside this test.

## Reproduction and provenance

The only external numerical input is the rounded scalar w from the baseline SCI a820d6c7 aggregate fit. The recurrence P is the published campaign clock. There is no new raw download or shared dataset path. Exact source identifiers, member hash, environment versions and job identity are in files/provenance.json. No raw observations or record-level extracts are bundled. See files/NOTICE_external_data.md.

With Python 3.12, numpy, scipy and matplotlib, run in a separate local output directory:

    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/path/to/scratch/output

For the independent checks, copy files/analyze.py and files/validate.py into a separate scratch directory and run validate.py there. It writes validation.json beside the copied script. Compare it with the supplied file. This takes minutes on one CPU. There is no random sampling. To inspect the scalar source:

    python files/retrieve.py /path/to/campaign /path/to/separate/scratch

This verifies the prior signed bundle and checks the member hash. It writes outside the signed publication. Preserve the cited SCI bundles if replay of the original fit is needed. The model computations themselves need no external files. The baseline license covers our code, narrative, synthetic outputs and figures. It does not change external data terms.
