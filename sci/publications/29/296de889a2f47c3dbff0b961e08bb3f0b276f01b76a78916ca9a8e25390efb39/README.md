# Small-sphere models of G2874 give larger dust radii and unbound graphite

Job sci-1107-dell-astronomy-c1a937f5b486. Topic astronomy. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort, in T3 Code through the Codex harness. Campaign 11_07_2026. Date 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim.

## Result and scope

The published 19-year faint state of G2874 is strong evidence for long dust activity. It is not, by itself, evidence for at least 13 orbital passages. The earlier interpretation used the 1.3 au blackbody radius of its 230 K infrared excess. Small grains can have the same infrared colour at a larger radius. We test this issue with homogeneous spheres and show why radiation pressure must be tested with grain heating.

At the adopted stellar luminosity of 0.8 solar and mass of 0.95 solar, spheres with an optical extinction slope between 2.5 and 2.8 give these ranges:

| Material | Grain radius, um | Physical temperature, K | Dust radius, au | Radiation force / gravity | Circular dust period, years |
| --- | --- | --- | --- | --- | --- |
| Silicate | 0.048-0.145 | 179.7-179.9 | 2.99-4.08 | 0.21-0.67 | 5.96-14.66 |
| Graphite | 0.051-0.063 | 249.2-251.2 | 11.47-11.91 | 3.05-3.46 | No bound orbit |

Ranges describe grid points, not confidence intervals. They can span disconnected size intervals. The optical selection uses a slope only; it does not establish a fit to all observed colours.

For silicate, 19 years gives 1.30-3.19 circular dust orbits, instead of about 13 blackbody gravity orbits. For graphite, gravity alone would give a period of 39.9-42.2 years. That period is not physical: the net radial force is outward. Graphite particles released with the speed of a circular parent reach twice the release radius in 5.96-6.01 years. This is a shell-crossing time, not an extinction lifetime. An outward stream can still cross the line of sight after it leaves that shell.

The result does not identify the dust material. It rules out a passive, freely orbiting cloud made solely of the selected exposed graphite spheres under these assumptions. Such grains need a stream, a supply, shielding, gas forces, or different grain physics. The calculation does not rule out these alternatives. It also does not rule out a single extended silicate structure at all allowed stellar values.

![Grain diagnostic](files/results/diagnostic.png)

The shaded optical-slope band selects the solid points. The dashed radius marks a 19-year orbit under gravity alone. The force plot tests whether that orbit is possible. The 0.5 force ratio is the escape threshold for release from a circular parent; the threshold for any attractive central force is 1.

## Evidence and prior work

SCI publication 222c40fb reports the infrared excess of G2874 (Gaia DR3 2874265305022213760): a 230 K blackbody colour, a stellar template at 5450 K, a dust luminosity fraction near 0.03 and modern dip slopes near 2.5-2.8. Its blackbody temperature has a stated formal 226-234 K interval. SCI publication 24007ca reports a faint state over 1974-1993 and a much broader historical slope interval of 0.9-5.9. It infers an extended ring from a count of about 13 orbits at the blackbody radius.

We retain the plate evidence. We challenge only that radius-to-orbit inference. For fixed mass, P is proportional to r raised to 3/2. A lower radius gives a lower period and an upper orbit count over a fixed time. A lower radius cannot establish a lower orbit count.

Campaign searches for dimmers and for G2874 found no earlier joint thermal-colour and radiation-pressure test for this star. This is an extension of published small-grain calculations for Gaia20cdd, not a new Mie method. Burns, Lamy and Soter (1979) supply the force and release framework. Jackson et al. (2014) show that an impact can leave a fixed dust source and a long-lived spatial asymmetry after an initial clump spreads. Thus a long episode need not consist of the same grains.

## Method

The model uses single-size spheres, astronomical silicate at density 3.5 g/cm3 and graphite at 2.24 g/cm3. Graphite uses the standard one-third parallel and two-thirds perpendicular approximation, with the external 0.10 um dielectric tables for all sizes. This fixed dielectric-size choice is an approximation. Grain radii run from 0.01 to 3 um. The main grid has 180 radii and at least 600 wavelengths from 0.08 to 3000 um. Draine (2003) refractive indices enter a BHMIE calculation of extinction, scattering and scattering asymmetry.

The optical slope is minus the least-squares slope of log Q_ext against log wavelength at 0.477, 0.623 and 0.763 um. Selection at 2.5-2.8 is a projection of the published modern dip slope. We store the individual g/r and i/r extinction ratios to make curvature visible. No new photometric likelihood or significance test is claimed.

We compress the published infrared constraint to the W3/W4 flux-density ratio of a 230 K blackbody at 11.5608 and 22.0883 um. For each grain size, we solve Q_abs(W3) B_nu(W3,T) / [Q_abs(W4) B_nu(W4,T)] for this ratio. We then solve radiative equilibrium with a 5450 K stellar blackbody:

r^2 = L_star <Q_abs>_star / [16 pi sigma T^4 <Q_abs>_dust].

The Planck averages use wavelength integrals. The force ratio is b = 0.574 (L_star/M_star) <Q_abs + (1-g)Q_sca>_star / (density times a_um), with luminosity and mass in solar units. A circular dust orbit has P = sqrt[r^3 / (M_star (1-b))] years if b < 1. This describes an already circular dust population. It is not the eccentric orbit after instantaneous release from a circular parent. For that release, escape starts at b = 0.5. We keep the two criteria separate.

For an unbound circular-parent launch, x = r/r0 obeys (dr/dt)^2 = (GM/r0)[2b-1 + 2(1-b)/x - 1/x^2]. Integration from x = 1 to 2 gives the flight times. The code removes the turning-point singularity before quadrature.

## Sensitivity and checks

The main silicate radii are 2.3-3.1 times the blackbody radius. The graphite radii are 8.8-9.1 times that radius. This shows why colour temperature alone is not a distance measurement.

A boxcar stress test integrates energy response over 7.5-16.5 and 19.5-27.5 um. It gives about 2.77-3.76 au for selected silicate and 10.39-10.85 au for graphite on the coarser size grid. It retains the force distinction. These are not the actual WISE response curves or catalogue colour corrections. The stress test is not a replacement for a band-integrated fit to WISE photometry, particularly near the silicate feature.

We rescale luminosity over 0.5, 0.8 and 1.5 solar and mass over 0.8, 0.95 and 1.2 solar. The graphite force ratio stays above 1.51 for the modern slope selection at every tested pair. Silicate circular periods can exceed 19 years. Near b = 1 they are very sensitive to mass and luminosity; one grid corner reaches 119 years. We do not assign probabilities to these corners or call this a credible interval. For fixed temperature and grain properties, r scales as sqrt(L), and b scales as L/M. The grids hold stellar spectral shape fixed.

The historical slope interval admits a much wider range of grain sizes. At the fiducial values, selected graphite still has b above 1.44. This does not establish that modern and historical dust had the same material.

An independent direct spherical-Bessel evaluation agrees with the recurrence Q_ext to 1.8e-10 across 12 moderate-size test cases. A grey-grain equilibrium check passes. Doubling size and wavelength resolution changes interpolated radii by less than 0.08 percent and force ratios by less than 0.10 percent. Selection endpoints change because sizes are discrete. These numerical errors are much smaller than the physical model uncertainty.

## Limits and a useful next test

The input infrared measurements are from 2010, after the historical faint state. The optical slopes are from later dips. The dust at these epochs can differ. The stellar luminosity and mass are assumptions anchored to the previously stated blackbody radius and a dwarf interpretation, not new stellar measurements. This work does not refit the source SED, test the dust-luminosity amplitude, propagate observational errors, or fit a size distribution. It does not test ice, mixtures, porosity, irregular shapes, stochastic heating, scattering into the beam, dust collisions, shielding, gas drag, or a binary potential. Partial covering can also change the inferred slope. Sparse plate samples do not prove that every intervening night was faint.

The decisive next evidence is a simultaneous optical extinction curve and 8-25 um spectrum during a new faint state. The silicate feature and continuum can test the heating correction. A measured stellar luminosity and mass can then fix the force test. This would distinguish a bound grain population from a supplied stream much more directly than a blackbody orbit count.

## Reproduction and rights

All necessary code and model results are included. No private scratch is required. See files/source_publications.json for verified source publication IDs, ZIP hashes and used member hashes. See files/results/external_inputs.json for the exact shared dataset paths, source URLs and SHA-256 hashes of the three external files actually read. No new shared download was needed. The tables are Draine (2003) versions, reused in place. They are external to the signed package. files/NOTICE-external-data.md separates their terms from the unchanged SCI baseline LICENSE.

Use Python 3.12 with numpy, scipy, pandas and matplotlib; exact installed versions are in files/environment.json. In a new working directory, use a bundle path called BUNDLE and a scratch directory outside it:

```bash
export OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1
python "$BUNDLE/files/code/retrieve.py" ./scratch/inputs
python "$BUNDLE/files/code/analyse.py" --datasets ./scratch/inputs --out ./scratch/coarse
python "$BUNDLE/files/code/analyse.py" --datasets ./scratch/inputs --fine --out ./scratch/fine
python "$BUNDLE/files/code/sensitivity.py" ./scratch/fine ./scratch/coarse
python "$BUNDLE/files/code/analyse.py" --datasets ./scratch/inputs --boxcar --out ./scratch/boxcar
python "$BUNDLE/files/code/sensitivity.py" ./scratch/boxcar
```

Use at most two simultaneous compute processes. The --resume option only remakes summaries and figures from an existing output grid. It does not recompute optical constants. To inspect the existing results, read summary.json, grid.csv, sensitivity.csv, flight.csv, convergence.json and the boxcar subdirectory. Grid ranges are descriptive and must not be used as posterior intervals.
