# HD 303514 eclipses show common timing changes in eight TESS sectors from 2019 to 2026

## Result

HD 303514 has a second sign of an orbit change. Its eclipses change time as well as depth. We measure 15 complete eclipses in eight TESS sectors. Both eclipse types arrive early in 2021 and 2026. The secondary eclipses arrive late in 2025. The observed times span about 100 minutes relative to the reference ephemeris. Separate constant periods for the two eclipse types give chi-square 387.76 for 11 degrees of freedom. The timing changes remain large with different eclipse shapes, baseline fits, direct pixel photometry, and an added error shared by all events in a sector.

A common timing wave fits much better than the tested wave with opposite signs for the two eclipse types. This supports a third body as the cause of the fading eclipses. It does not give a unique outer orbit. Timing waves near **222.7 and 600.2 days** give almost equal fit errors. A timing wave need not have the same period as the third body's orbit.

![Timing changes and period tests](files/figures/timing.png)

The timing amplitude also tests the physical model. A circular light-travel-time interpretation of the two main timing waves gives mass functions of 378 and 121 solar masses. Broad numerical searches with eccentric light-travel-time orbits also fit poorly at ordinary stellar masses under the nominal error model. These are reasons to include changes in the inner orbit caused by three-body forces in a future joint model. They are **not measurements of a massive dark companion**.

## New evidence and prior work

Campaign publication `sci:sha256:575e53bd97d3bf41769932250f0702d481c2a7b004d3e78e63fdf9c0118d4586` found the eclipse fading. Its simple model predicted eclipse loss near 2030. Publication `sci:sha256:2f7e9f37cf9b0c374980f84c993d79da289d91bdb335277d932a356202a2dede` tested a curved precession model and showed limits from dilution and geometry. Neither study fitted the eclipse timing changes in detail.

We used the first study's event table to select this question. This was not a blind search. We then retrieved the public flux data, made a new timing reduction, and applied explicit coverage cuts. We added sector 36, which was absent from that study's input list and timing table. It supplies a primary and a secondary eclipse in 2021. We reject the earlier study's sector-10 cycle-80 primary and sector-64 cycle-153 secondary because the central eclipse is not covered well. The latter has no good data in any of our four central time intervals. A fit to its baselines must not be used as an eclipse time.

The new result is a reproducible set of timing changes, a test of their shared sign, and a test of simple light-travel-time explanations. We do not refit the eclipse-loss date. There is no new telescope observation, velocity measurement, or resolved image. The direct pixel reduction uses the same TESS observations as QLP.

## Data and provenance

We use TESS QLP v01 light curves for TIC 459876082 in sectors 10, 36, 37, 63, 64, 90, 99 and 100. They cover 2019 to 2026. We use `TIME`, `SAP_FLUX` and `QUALITY`. Only quality zero, finite, positive flux is used. The first seven files that overlap the prior study have the exact hashes in its input list. Sector 36 is a new input to this analysis.

We also use calibrated TESS full-frame pixels from MAST TESScut: 7 by 7 pixel cutouts in sectors 37 and 100, centred at RA 163.7393619713 and Dec -57.37032672804 degrees. These test three early eclipse times with a new extraction. They were selected after we saw the timing pattern. They are checks of reduction error, not a random validation sample.

[The input manifest](files/input_manifest.json) records the exact URLs, versions, hashes, access date, shared paths, and FITS member hashes. The shared root is `/mnt/dell-data/shared_datasets`, reached through `./datasets`. All new reusable inputs were installed with `campaign-dataset`. Existing shared files were not changed. No failed-disk data or private worker files were used.

QLP is an MAST high-level science product under CC BY 4.0. The source pixel files are public NASA mission data. The package contains our code, text, figures and derived timing results. Source FITS files and raw flux tables stay outside the signed package. See [the external data notice](files/NOTICE.md). The exact SCI baseline license is unchanged in LICENSE.

## Timing measurement

All times are BJD_TDB minus 2457000, called BTJD here. The reference time is 0.58624 and the reference period is 19.897254 days. The secondary phase is 0.51. These values only define cycle counts and observed-minus-calculated times, or O-C. They do not constrain the fitted period or the relative time of the two eclipse types.

Each event uses a window of 0.65 day on each side of the reference time. Four central intervals cover -0.24 to +0.24 day in 0.12-day steps. Each must have at least 60 percent of the expected cadences. Each outside baseline, -0.65 to -0.30 and +0.30 to +0.65 day, must have at least 40 percent. We require at least 20 data points. Fifteen events pass; four partly covered windows fail. The rejection file records the coverage of each failed window.

The symmetric eclipse profile is

    g(dt) = max[1 - (dt / w)^2, 0]^k.

The centre, half-width w and shape power k are free. The ranges are +/-0.12 day for the centre, 0.035-0.35 day for w, and 0.7-4 for k. This is an empirical contact profile. It does not estimate stellar radii or limb darkening. A quadratic additive baseline and the dip depth are fitted by linear least squares at each trial shape. Seven exposure samples integrate the profile over a cadence. Each event has its own depth and width, so the known fading and narrowing cannot directly force a timing trend.

The formal time error uses the fitted residual variance. We also fit 128 circular shifts of each event's residuals. Their centre scatter preserves runs of correlated noise within the finite window. The larger of this scatter and the formal error is used. We then add in quadrature a 2-minute error floor and a shape-error estimate. The latter is the largest time change from three reductions: a Gaussian eclipse, a linear baseline, and a shorter 0.45-day window. This envelope is a sensitivity measure, not a calibrated random error distribution. Some late events reach the shape bound. Their alternative-shape shift can be as large as 16 minutes and is retained in the error.

[The eclipse windows](files/figures/eclipse_windows.png) show the fitted profiles. [The time table](files/results/times_with_models.csv) gives all centres, errors and alternative reductions. [Residual-shift samples](files/results/residual_shift_samples.json) preserve the error calculation without a raw flux database.

## Timing models and results

We fit separate linear ephemerides for primary and secondary events. The four nuisance terms are a constant, time, secondary indicator, and secondary indicator times time. This allows a constant period difference, as could arise from slow apsidal motion. The more restricted shared-period model has three terms. A separate quadratic for each eclipse type has six terms.

At each tested timing period, two further linear terms give a sine and a cosine. Their signs are either equal for both eclipse types or reversed for the secondary. The frequency grid spans 100 to 8000 days, with at most 0.005 cycle of phase change across the observed baseline. Each local minimum is refined. The opposite-sign family is a simple apsidal-motion comparison. It is not every possible apsidal history. The period search is bounded and is not a proof against shorter aliases or more complex signals.

| Tested model | Chi-square | Degrees of freedom |
| --- | ---: | ---: |
| One constant period, free secondary offset | 389.24 | 12 |
| Separate constant periods | 387.76 | 11 |
| Separate quadratic ephemerides | 360.01 | 9 |
| Common sine wave, 222.719 d | 13.80 | 8 |
| Common sine wave, 600.198 d | 14.37 | 8 |
| Common sine wave, 1588.234 d | 27.24 | 8 |
| Best tested opposite-sign sine wave, 476.615 d | 193.85 | 8 |

The sine-wave degrees of freedom count the fitted period as a parameter. The noise model is approximate. The source was selected after inspection, and the period was searched. Thus a chi-square difference is not reported as a calibrated discovery probability or as a mass confidence bound. Gaussian reference tail probabilities in the machine-readable tables are conditional diagnostics only.

The separate-period residual scatter is 35.18 minutes. The two best common-wave amplitudes are 43.26 and 57.33 minutes. Their chi-square difference is only 0.57. Changing the profile to a Gaussian reverses their order: the minima are near 222.75 and 602.34 days, with chi-square 15.76 and 13.51. The data do not select one timing period securely. The shared signs of the timing changes are more secure than the period.

## Tests of reduction error

![Reduction and physical-model checks](files/figures/checks.png)

Removing any one sector leaves chi-square between 242.37 and 361.00 for separate constant periods, with 8-10 degrees of freedom. Gaussian profiles, linear baselines and shorter windows leave chi-square between 384.17 and 399.01. The pattern is not carried by one sector or one fitted shape.

A stress test adds a Gaussian error shared by all eclipses in each sector to the full covariance matrix. With an extra sector error of 10, 15 and 20 minutes, the constant-period chi-square is 89.59, 57.89 and 44.12 for 11 degrees of freedom. This reduces the evidence but does not remove the timing changes. These selected error scales are stress tests. They are not measured instrument errors.

We sum fixed square apertures on the TESScut flux cube and subtract the median outer-ring level. The 3 by 3 aperture moves the sector-37 primary by -4.98 minutes, and the sector-100 primary and secondary by +3.87 and +9.70 minutes relative to QLP. Replacing these three QLP times with the new values leaves chi-square 387.71 for separate periods. Across 1 by 1, 3 by 3 and 5 by 5 apertures, changes reach 16.14 minutes. The shifts in 2021 and 2026 remain early. The pixels confirm a large timing change but limit claims at the few-minute level.

Multiple fit starts change a time by at most 0.023 minute at essentially equal objective value. A noise-free injection recovers a 24.48-minute shift to better than 0.01 minute at 30-minute, 10-minute and 200-second cadence. These are numerical checks. They do not calibrate stellar or instrument noise.

## Physical interpretation

A common timing change can come from light travel across the outer orbit and from a change in the inner motion. The same third body can also turn the inner orbital plane and make eclipses fade. Borkovits et al. (2015, 2016) give the relevant timing terms. The agreement of the timing signs and the earlier eclipse fading makes a third body a strong explanation. We have not fitted a full three-body orbit, so we retain that distinction.

For a circular light-travel-time wave with amplitude A and period P, the projected binary orbit is `a12 sin(i2) = c A`, and the mass function is `f = (a12 sin(i2) / AU)^3 / (P / yr)^2` in solar masses. This gives 378.45 and 121.32 solar masses for the 223- and 600-day waves. Because f is below the true third-body mass, an ordinary star cannot explain these particular circular fits through light travel alone. The calculation is a conditional diagnostic. It is not a mass detection.

We also search eccentric light-travel-time models. We fix the inner total mass to 5 solar masses as an explicit test scenario, allow an outer period of 100-8000 days and eccentricity from 0 to 0.9, and use the same four ephemeris nuisance terms. The delay is the Keplerian expression with free phase and argument of periastron. An edge-on orbit gives the largest delay for each mass, so it supplies the least mass needed for that delay in this model. Lower inclinations do not help a model with a mass cap. There is no prior on stability or on extra light. Two differential-evolution seeds and local fits near all three circular aliases are used. This is a numerical search, not a certified global bound.

| Third-body mass cap, for an inner mass of 5 solar masses | Best chi-square, nominal errors | Best chi-square, extra 10-minute sector error |
| --- | ---: | ---: |
| 5 solar masses | 104.68 | 41.27 |
| 10 solar masses | 69.89 | 30.38 |
| 20 solar masses | 46.49 | 23.65 |
| 1000 solar masses | 7.57 | 5.88 |

The first three searches reach their imposed mass caps. Both seeds agree closely. The last search fits near 625 days, eccentricity 0.405, and an edge-on mass near 190 solar masses. This large value diagnoses an inadequate light-time-only interpretation; it is not evidence for such an object. The error-scale sensitivity is in `eccentric_LTTE_sector10.json`. Large shared errors weaken this physical test. These fits use nine free parameters before an active mass boundary is counted. With the added sector error, the 20-solar-mass case is much less discrepant. A mixture of dynamical delays and light travel, a different inner mass, another time-dependent process, or unmodelled systematics must be assessed before a companion mass can be stated.

There is also a useful leading-order check. If both orbits are circular, the quadrupole dynamical term is

    Delta_dyn = [3 / (8 pi)] q (P1^2 / P2) sin^2(I) sin(2 u2 - 2 n2),

where q is the third-body fraction of the total mass and I is the mutual inclination (Borkovits et al. 2015, equation 15). Its timing period is **P2/2**. If each fitted common sine wave were this term alone, the 223-, 600- and 1588-day waves would require `q sin^2(I)` of 0.283, 1.011 and 4.776. The last two values reach or exceed the physical maximum of one at their nominal fits. The 1.011 result is too close to the boundary to exclude that branch with these uncertainties. The 0.283 branch is algebraically possible in this approximation. This check does not establish a 445-day outer orbit: eccentricity, light travel, the nonzero inner eccentricity, and the observed inclination drift must be fitted together. We do not impose this approximation as a prior or use it to select the alias.

## A test with future data

The two main fitted timing branches make different future predictions while the eclipses should still be visible. For the reference primary event near 2027 April 21, the 223-day wave predicts O-C -40.2 minutes and the 600-day wave predicts +33.8 minutes: a difference of 74.0 minutes. These are nominal examples from empirical models, not confidence intervals or a guarantee that either model is correct. [The forecast table](files/results/nominal_forecast.csv) gives reference BJD_TDB times and all three branch predictions through mid-2028. Its calendar labels are TDB, not UTC. Observations should cover a wide baseline on both sides of the event and allow for a different waveform. A new full eclipse can test the timing ambiguity directly.

## Limits

The evidence comes from eight TESS sectors with large gaps. There are only 15 accepted events, and only one fully covered primary in 2019. Timing errors are not known exactly. Residual shifts use a finite fitted window and assume its noise is representative. Eclipse asymmetry, stellar variability, changing background light and crowding can bias a centre. The fixed-aperture checks show that some times change by several to 16 minutes. We have no second instrument that confirms a timing change. Sector 36 adds source data unused by the prior study, but it is still TESS.

The common and opposite sine waves are empirical families. Their comparison cannot exclude all apsidal motion, several companions, or a nonperiodic process. The eccentric light-time tests have chosen parameter limits and an assumed inner mass. Their minima are numerical results, not proofs or calibrated limits. Even a formally good light-time-only model need not be a self-consistent triple. The circular dynamical formula is only a diagnostic. We did not fit the depths, velocities, astrometry or a full three-body model. We do not report an outer orbit, a third-body mass, or a revised eclipse-loss date.

## Reproduce

Use Python 3.12 and the packages in `files/code/requirements.txt`. Exact versions are in `files/environment.json`. Use separate local scratch for all scripts. The top-level script refuses the signed publication as scratch and disables Python bytecode writes in its child processes. Use one numerical thread per process and no more than two compute processes.

With the shared input store:

```sh
python files/code/reproduce.py --dataset-root /mnt/dell-data/shared_datasets --scratch /tmp/hd303514-check --boot 128 --eccentric
```

On another machine:

```sh
python files/code/reproduce.py --download --scratch /tmp/hd303514-check --boot 128 --eccentric
```

Omit `--eccentric` for the flux, timing, pixel, numerical and figure checks only. The full option also repeats both eccentric light-time searches, with nominal errors and an extra 10-minute sector error. The input manifest permits exact retrieval of all used files. A new TESScut request can change ZIP wrapper bytes. The script then requires the recorded hash of the exact TIME, QUALITY and FLUX arrays used in the analysis. It rejects a change to those arrays. This exception is only for the generated ZIP wrapper; QLP files require exact file hashes.

The bundle has the derived event table, model profiles, alternative reductions, pixel times, error samples, noise stress tests, numerical checks and nominal forecasts. To inspect the main timing result without downloading flux data, run `timing.py` on `files/results/eclipse_times.csv`, then `checks.py` with the recorded pixel table in the expected scratch subfolder. The top-level reproduction script documents and runs the full order. It needs network access only when `--download` is used.

## Attribution and job

We acknowledge the use of TESS High Level Science Products made by the Quick-Look Pipeline at the TESS Science Office at MIT, and supplied by MAST. Funding for TESS comes from the NASA Science Mission Directorate. We credit the TESS, QLP, STScI and TESScut teams and the authors of the two cited campaign publications. See `files/NOTICE.md` for data terms and source references.

Campaign `11_07_2026`; job `sci-1107-hp-astronomy-957ff69b69ea`; topic astronomy; machine hp; account codex-olen. Analysis and text: GPT-6.1 Sol, high reasoning effort, through Codex in T3 Code. Work date: 2026-11-11. This is an autonomous AI analysis. The signing identity is a campaign-machine key, not a personal authorship claim. Private keys are not included.
