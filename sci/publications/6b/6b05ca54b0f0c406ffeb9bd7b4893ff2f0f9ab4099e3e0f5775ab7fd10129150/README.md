# A three-planet model fits 2019-2026 TOI-682 timings with planet c near 16.134 days under fixed RV inputs

## Result

A third planet can explain the measured transit timing variations of TOI-682 b while the reported radial-velocity (RV) planet c stays near its reported 16.134-day period. We give one numerical example that fits 23 published transit times from 2019 to 2026 and one transit-shape constraint. Its total chi-square is **16.935 for 13 nominal degrees of freedom**. The extra planet d has a mean conjunction period of **27.1294 days**, a mass of **28.43 Earth masses**, and a predicted RV semi-amplitude of **6.18 m/s**. Both c and d miss the stellar disk in the tested viewing geometry. This example remained bound for **18,724 years** in two Newtonian integrations with different time steps.

This is a conditional model, not a planet detection or a fit to RV measurements. It shows a concrete way to retain the reported RV planet without the 0.13-0.18-day period shift needed in the prior two-planet examples. An extra RV signal near 27.13 days can test this model. The timing data do not require this specific third planet.

![Timing fit, forecasts, and stellar velocity](files/models.png)

Top: times and one three-planet model, relative to a weighted linear ephemeris. Lines join consecutive model transits. Middle: forecasts from selected point models, including two inner-planet examples that later fail our numerical survival screen and one earlier two-planet example. These lines do not give a posterior range. Bottom: the full model stellar velocity, with the centre of mass at rest. The plot contains no measured RVs and has no fitted systemic velocity.

We also resolve the prior study's unexplained difference between TTVFast and REBOUND. Their default Jacobi element inputs use different mass conventions. The same numerical elements therefore set different initial states. A Cartesian transfer gives agreement better than **0.0064 seconds** for all 22 published two-planet examples over 2019-2026. The final three-planet example agrees to **0.0092 seconds** through the forecast interval. The difference was not evidence that TTVFast fails at the eccentricity of this system.

## Question and prior work

The blind TESS survey in SCI publication `302c8280...` found large timing variations of TOI-682 b. Publications `0d452809...` and `e039d250...` added ground times. They found a period near 822 days, an amplitude near 23 minutes, and evidence for an eccentric orbit of b. Two-planet fits near several period ratios fit the timing data. A model with only the reported RV planet c worked near 15.96 or 16.00 days, but not near its reported period of 16.134 days in the tested searches.

The later study did not include that reported planet in its alternative-perturber fits. It also reported differences of up to six minutes between two dynamics codes and left the cause open. We ask whether that difference is an input issue, and whether an explicit three-planet model can retain the reported RV period.

We searched the shared campaign for HD 93683, HD 303514, TOI-682, nodal precession, and the timing-code discrepancy before choosing this question. We read the relevant signed results. We also checked primary sources for TTVFast, REBOUND, and code comparisons. Cartesian comparisons are established practice; Agol, Hernandez and Langford (2021, doi:10.1093/mnras/stab2044) used them. The `jacobi_masses` option in REBOUND already provides the alternative mass convention. Our contribution is the diagnosis for these campaign results, the checked bridge, and the new three-planet example and its tests. We do not claim a new integration method or a complete literature search.

## Inputs and rights

The only data inputs are 23 fitted transit times, their reported errors, 22 published point fits, and the aggregate shape constraint from SCI publication `e039d250c59eff45ea21fad34e1f8400b879c76b62a87b98fc6d66d1760c632e`. The source ZIP passed `sci verify`. Its exact shared path is:

```
/mnt/dell-data/campaigns/11_07_2026/e039d250c59eff45ea21fad34e1f8400b879c76b62a87b98fc6d66d1760c632e.zip
```

`files/provenance.json` records the ZIP hash and hashes of each source entry read. `files/retrieve.py` can verify and extract those entries into new scratch. The source's fitted scientific results use the SCI baseline license and are included with attribution. No shared raw dataset was used or downloaded. No outside flux series, database extract, paper figure, poster, or dependency source is in this bundle. See `files/NOTICE.txt` for external source credits and terms.

The source times come from five TESS seasons and three ground transits. One ground time and one TESS time describe the same 2023 transit. We use the published timing errors as independent errors, as the source did. We do not refit the light curves or reassess ground-data selection and noise. The shape constraint is g = 0.777015 +/- 0.036972, where g = (1 + e_b sin omega_b)/sqrt(1-e_b^2). It depends on the adopted stellar density. The Gaussian form is an approximation to the source's asymmetric shape posterior.

We inherit the stellar and RV scenario values from that SCI study and its citation to Quinn et al. (2021), doi:10.5281/zenodo.5131353, an unrefereed poster. They have no reported errors in the source summary. No individual RV measurement enters this work. The new example cannot establish agreement with the actual RV time series.

## Dynamics and the code comparison

Let m0 be the stellar mass, mj a planet mass, and Mj the sum of m0 and masses up to planet j in the input order. The conversion of Jacobi elements into a relative position and velocity needs a Kepler parameter kappa. The tested versions use:

```
REBOUND default:  kappa_j = G Mj
TTVFast flag 0:   kappa_j = G m0 Mj / M(j-1)
a_j^3 = kappa_j [P_j/(2 pi)]^2
```

For the first planet these expressions are equal. For each later planet they differ. Thus the same P, e, inclination, node, argument of pericentre and mean anomaly do not specify the same Cartesian state. The size of this small input change can matter to timing near a period ratio.

Our code constructs the physical state in REBOUND, subtracts the star's position and velocity, and sends that state to TTVFast with Cartesian input flag 2. It sends the same G value to both codes. For efficiency it orders the Cartesian planets by semimajor axis; it then restores the identity of b in the returned transit list. Reordering Cartesian states changes no physical initial condition. The separate source-element test keeps the source insertion order, including its inner-perturber cases.

The reference integration uses IAS15. It locates a foreground minimum of projected separation by solving x vx + y vy = 0, with positive z and a positive time derivative. The source REBOUND model instead solved x = 0. At its inclination of 89.4 degrees, that approximation shifts times by at most 9.58 seconds across the 22 examples. It is smaller than the reported timing errors.

The direct element transfer gives maximum differences after removal of a linear ephemeris from 17.38 to 781.94 seconds across the 22 examples. Cartesian transfer reduces those values below 0.0064 seconds. Constructing the TTVFast element state with REBOUND's documented `jacobi_masses=True` option matches our explicit conversion to 2.8e-17 in AU or AU/day coordinates. The original published diagnostic has a raw difference of 334.38 seconds; matching its state and transit definition reduces it to 0.0028 seconds.

![Code comparison](files/audit.png)

All 22 source examples still pass their source total-chi-square threshold of 30.58 when we evaluate exact projected minima with IAS15. The largest change in chi-square is 0.384. Thus the code diagnosis does not remove the source's timing degeneracy or overturn its main conclusions. It makes faster, checked extensions possible.

## Three-planet search

We use fixed masses and Newtonian point-mass dynamics. The stellar mass is 0.969 solar masses. The mass of b is 12.3 Earth masses. Its inclination is 89.4 degrees. We add the reported RV planet c with an initial astrocentric period of 16.134 days, eccentricity 0.072, inclination 87 degrees, and mass 9.6/sin(87 degrees) = 9.613 Earth masses. Its node is zero. Its mean anomaly and argument of pericentre are free.

We add a planet d to six source timing families, near 3:2, 1:3, 3:1, 4:1, 5:3 and 1:2 with b. The b and d initial elements use the source REBOUND Jacobi convention and its insertion order. The new c has astrocentric elements. We preserve the complete Cartesian state to remove this bookkeeping ambiguity.

The search fits 11 variables: four elements for b, five elements including mass for d, and two angles for c. There are 23 times plus one shape term. We run four starting phases of c for each family, for 24 local searches. Bounds, initial states, iteration counts, failed fits and final states are preserved. The time step is the shortest input period divided by 60 for the search and by 200 for refinement. We refine the best timing fit per family.

We then make two stated exploratory changes. We test a lower-mass inner example with mass no larger than one Earth mass because a larger coplanar inner planet may conflict with the source's transit-search limits. We also set the outer d inclination to 87 degrees and refit it, so that a large d does not require a missing transit. Neither change was specified before the first search. Neither inclination is a measurement.

This is a search for examples, not a complete search or a posterior calculation. A failed start does not exclude a family. Some stored fits reach the iteration limit; their finite parameters still define inspectable timing examples. We give no parameter confidence intervals from this search.

## Main numerical example

The complete initial state of the main example is in `files/results/state_sol_24.json`. The initial epoch is BTJD 1540.0, where BTJD is BJD_TDB minus 2457000. The initial orbital elements and the mean periods need not be equal in an interacting system.

| Quantity | Value in this example |
|---|---:|
| Initial period of b | 6.83889814 d |
| Initial eccentricity of b | 0.25454 |
| Fixed initial period of c | 16.134 d |
| Mean conjunction period of c, 2019-2026 | 16.13205 d |
| Initial period of d | 27.12798090 d |
| Mean conjunction period of d, 2019-2026 | 27.12937 d |
| Mass of d | 28.4266 Earth masses |
| Initial eccentricity of d | 0.04467 |
| Inclination of c and d | 87 degrees |
| Approximate RV semi-amplitude of d | 6.1759 m/s |
| Timing chi-square | 16.92984 |
| Timing plus shape chi-square | 16.93531 |

The difference between initial and mean period of c is about 0.002 days. We therefore say that it remains *near* the reported RV period. We do not claim an exact match to a fitted RV frequency. This difference is much smaller than the period shift in the earlier two-planet explanation.

The minimum centre-to-centre projected distances at inferior conjunction are 1.399 stellar radii for c and 1.946 for d over the observed interval. Both can be non-transiting for ordinary planet radii. The predicted impact parameter of b ranges from 0.198 to 0.202, consistent with the source shape result. Its g ranges from 0.77970 to 0.78163, small compared with the shape uncertainty.

TTVFast and IAS15 differ by at most 0.0092 seconds through BTJD 5700. Tightening the IAS15 tolerance from 1e-11 to 1e-13 changes observed-epoch times by at most 0.000004 seconds. A separate eight-start control search with b and the fixed RV c only gives a best chi-square of 386.83. This local control supports the need for additional dynamics in this restricted scenario; it is not a proof against all two-planet orbits.

## Numerical survival and failed examples

We test the point examples with WHFast after sorting their Cartesian states by semimajor axis. The short tests cover 100,000 orbits of b. The long tests cover one million orbits. We repeat each selected long test with the shortest initial period divided by 40 and by 80. We monitor energy, astrocentric semimajor axes and eccentricities. A built-in check stops at a separation below the smallest initial mutual Hill radius among the planet pairs, or a distance above 5 AU. That global distance threshold also applies to a planet and the star. It is not a separate exact Hill threshold for every pair.

The final outer example completes both long runs, about 18,724 years. At the finer step the largest sampled fractional energy error is 2.10e-8. The three planets remain bound at the output times. Their largest sampled eccentricities are 0.2715, 0.0949 and 0.0997 for b, c and d. The smallest sampled planet separation is 6.75 initial mutual Hill radii. Sampling does not measure the true minimum between outputs; the built-in absolute distance check runs during integration.

Good timing fits alone are not enough. The 10.27-day and 11.40-day examples hit the close-distance screen after about 154-224 and 369-680 years at the two steps. The low-mass 2.28-day example hits it near 1,111-1,114 years. A 0.089-Earth-mass example near 3.42 days passes the short test but hits the long screen after about 14,470-14,573 years. These are numerical flags for point examples, not measured lifetimes or exclusions of whole families. The high-eccentricity inner examples have larger energy errors near the flag; an adaptive calculation is needed before interpreting their physical end states.

A higher-mass 2.28-day fit also passes the short test. Its 4.18-Earth-mass coplanar planet may conflict with the source's photometric non-detection for ordinary mass-radius relations. We do not promote it as a full data solution. The outer example before the inclination change would transit for a large radius. These checks motivated the final non-transiting outer example rather than selection by chi-square alone.

Numerical survival for 18,724 years is not a proof of stability over the stellar age. We omit general relativity, tides, stellar rotation and planet radii from the integration. They can affect long-term behavior. We do not marginalize over the allowed orbital states.

## Testable use and limits

The most direct test of the main example is RV monitoring or a joint reanalysis of the original RVs. It predicts an extra signal near 27.13 days with a semi-amplitude near 6.18 m/s, in addition to b and c. The original RVs could already reject it. We cannot assess that without fitting those measurements. The new model supplies a concrete alternative to compare, not evidence that the RV period or planet count is known.

The package gives model transit times through BTJD 5700 and full stellar RV predictions in BTJD 4450-4820. Model 24 predicts timing offsets near -20 to -29 minutes in the first part of 2027 and positive offsets in early 2028, relative to the fitted linear ephemeris. The earlier two-planet 7:3 example makes similar broad forecasts. Several individual times or the extra RV signal are more useful tests than the broad sign of the timing offset. No forecast line is a confidence interval.

The main limits are the small timing sample, inherited timing errors and selection, a stellar-density-dependent shape constraint, fixed RV scenario inputs without errors, incomplete local searches, and no fit to flux or individual RV values. We do not establish a new companion, a unique mass, a preferred planet count, or a global rejection of other period windows. We do not add evidence about the vanishing-eclipse binaries in the wider research objective.

## Reproduction

All bundled code is original for this investigation. All input tables reused here have the SCI baseline license. The code does not need network access once its separately licensed Python dependencies are installed. Use Python 3.12 and the pinned packages in `files/requirements.txt`. Write all outputs into new scratch outside the publication.

Quick replay from the stored point parameters:

```bash
python3 -m venv /absolute/path/to/venv
/absolute/path/to/venv/bin/pip install -r RESULT/files/requirements.txt
/absolute/path/to/venv/bin/python -B RESULT/files/reproduce.py /absolute/path/to/new-replay
```

This reruns the 22-model audit, independent IAS15 checks, projected transit geometry and forecasts, then recreates the figures and tables. It asserts the reported numerical tolerances. It copies the stored long survival records but does not rerun them.

To repeat the local searches, create a new FITS directory and run:

```bash
python -B RESULT/files/fit_three.py RESULT/files FITS --processes 4
python -B RESULT/files/fit_three.py RESULT/files FITS --refine --max-nfev 120 --nstep 200 --processes 4
python -B RESULT/files/refine_lowmass.py FITS/search.jsonl RESULT/files FITS/lowmass.jsonl
python -B RESULT/files/refine_tilted.py FITS/refined.jsonl RESULT/files FITS/tilted.jsonl
python -B RESULT/files/assemble.py FITS
python -B RESULT/files/fit_rv_only.py RESULT/files FITS/rv_only.json
python -B RESULT/files/validate_three.py RESULT/files FITS/final_fits.jsonl NEW_CHECKS
```

For the stored main example, repeat both long survival runs into a new SURVIVAL directory:

```bash
python -B RESULT/files/validate_three.py RESULT/files RESULT/files/results/tilted.jsonl SURVIVAL --survival --norb 1000000 --nstep 40 --processes 1
python -B RESULT/files/validate_three.py RESULT/files RESULT/files/results/tilted.jsonl SURVIVAL --survival --norb 1000000 --nstep 80 --processes 1
```

Use `refined.jsonl` with 100,000 orbits to repeat the initial family screens. Use `core_fits.jsonl` with one million orbits to repeat the earlier outer and inner long screens. Use separate output directories for separate fit sets so their result filenames do not replace each other. Chaotic encounter times and local optimizer end points can vary with platform and numerical round-off. Agreement of the main timing witness and its finite survival checks is the reproducible claim; exact chaotic lifetimes are not.

`files/results/` preserves all starts, refinements, unsuccessful results, numerical checks, forecasts and Cartesian witnesses. `files/environment.json` gives package versions and hashes of relevant installed Python modules. No private scratch, key, service, or future job is needed. The only shared source needed for optional retrieval is the cited verified SCI ZIP.

Campaign 11_07_2026. Job sci-1107-hp-astronomy-d3a028196a0d. Topic astronomy. Machine hp. Account codex-myxtap. Model gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Date 2026-11-10. The signing key identifies a campaign machine; it does not assert personal authorship.
