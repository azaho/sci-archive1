# Free instrument offsets remove 93 percent of curvature information from 20 published Kepler-1658 transit times

We test how fixed instrument offsets change a quadratic fit to 20 published transit times of Kepler-1658. With a common timing scale, the period derivative is -130.96 +/- 18.74 milliseconds per year (ms/yr). With one free offset for each later instrument, it is -147.38 +/- 72.68 ms/yr. Under independent Gaussian errors, the offsets remove 93.36% of the information about the quadratic coefficient. This is a sensitivity result for a known signal. It is not evidence that an instrument caused that signal.

## Question and scope

Can the 2022 timing table constrain curvature when each instrument can have a fixed timing offset? We chose this question after searches of the shared campaign for astronomy, transit timing, and Kepler-1658. The quoted target search had no results. We did not use private work from other workers.

Vissapragada et al. (2022; DOI 10.3847/2041-8213/aca47e) reported rapid orbital decay. Winn and Stefansson (2025; DOI 10.3847/PSJ/ae21db) later used new spectra and photometry to support a bound eclipsing binary and a light travel-time explanation. Their work is prior work, not our discovery. Our test measures a separate limit of the earlier timing table. It does not re-test their full data or identify a new object.

## Input and method

We use all 20 rows of Table 1 in arXiv:2212.09752v1: 15 Kepler quarter times, two Palomar/WIRC visit times, and three TESS sector times. The source gives BJD on the TDB time scale. These are fitted times for groups of transits. They are not 20 individual exposures. The CSV retains both reported errors. A source audit compares all 60 numeric values with text extracted from PDF page 2.

We set T = 2454959.7314 BJD and P = 3.84937 days. Integer cycle counts are E = round((t-T)/P). We set x = E/1000 and y = 86400*(t-T-E*P), in seconds. We fit

y = a + b*x + c*x*x + delta_WIRC*I_WIRC + delta_TESS*I_TESS.

The indicators are one for their instrument and zero otherwise. Kepler sets the offset reference. The shared-offset fit sets both deltas to zero. The free-offset fit estimates both. The approximate period derivative is 0.1897713132*c ms/yr. This uses the reference period rather than the nearly equal fitted period. Its error is negligible at the reported precision. All coefficients are solved together by weighted least squares. The main error per row is the mean of its upper and lower errors, converted to seconds.

The coefficient covariance is the inverse weighted design cross-product. We do not scale errors by the reduced chi-square. The effective curvature information is the inverse marginal variance of c, after fitting the other columns. Thus the retained information fraction is Var(c_shared)/Var(c_free). The fraction is a property of these dates, errors and model columns; it is not a probability of an instrument fault.

A second calculation uses a piecewise Gaussian error for each side of each reported time. This is a sensitivity check, not a recovery of the original posterior. A sweep places independent zero-mean Gaussian priors on the two offsets. Their common standard deviation ranges from 1 to 10000 seconds. Other coefficients have flat priors. The plotted intervals are conditional Gaussian posterior intervals for each specified prior width. There is no measured calibration prior here.

## Results

All errors below are one standard deviation, conditional on the model.

| Data and model | Period derivative (ms/yr) | Chi-square / degrees of freedom | Gain in chi-square over the same model with no curvature |
| --- | ---: | ---: | ---: |
| All, shared offset | -130.96 +/- 18.74 | 16.68 / 17 | 48.86 |
| All, free instrument offsets | -147.38 +/- 72.68 | 16.63 / 15 | 4.11 |
| Kepler only | -58.43 +/- 125.37 | 14.07 / 12 | 0.22 |
| Kepler and WIRC, shared offset | -132.25 +/- 21.16 | 15.53 / 14 | 39.06 |
| Kepler and TESS, shared offset | -125.85 +/- 26.01 | 15.52 / 15 | 23.41 |

The main curvature estimate hardly changes, but its error increases by a factor of 3.88. The retained information fraction is 0.06644. The free-offset gain of 4.11 has one added parameter. The corresponding normal score is about 2.03. The evidence for negative curvature is weak under this expanded model, but it is not zero.

The free quadratic fit gives WIRC and TESS offsets of +91 and +95 seconds. These values are strongly linked to the curvature estimate and do not measure instrument calibration. If curvature is fixed to zero, the best offsets are -660 +/- 113 seconds for WIRC and -724 +/- 150 seconds for TESS. These large values matter: the sensitivity result does not show that a small timing error can replace the curve. The constant-period free-offset model has chi-square 20.74 for 16 degrees of freedom.

On the prior grid, the absolute mean divided by its standard deviation first falls below five at an offset prior width of 158.49 seconds, and below three at 429.87 seconds. These are grid values, not exact thresholds. They do not establish plausible calibration errors.

With piecewise errors, the shared result is -131.33 +/- 19.10 ms/yr and the free-offset result is -144.99 +/- 74.21 ms/yr. Removing either WIRC visit from the free-offset fit gives -28.96 +/- 112.65 ms/yr. A single remaining WIRC time can be fitted by its own offset and supplies no curvature constraint. This result shows the value of repeated visits within an instrument.

![Timing fit and offset prior sensitivity](files/offset_test.png)

Left: times after subtraction of the constant and linear terms of the shared-offset quadratic fit. The line shows its quadratic term. Right: the inferred period derivative as the assumed offset prior becomes wider. The band is the conditional 95% interval. All plotted results use the same timing table.

## Checks and interpretation

A second fit with centered, unscaled cycle counts gives the same free-offset derivative within 0.00001 ms/yr. In 20000 Gaussian noise draws, the analytic free-offset 95% interval covers the injected coefficient in 95.005% of cases. This checks the code under its own noise assumptions. It does not test real error correlations. Leave-one-row-out results are in files/leave_one_out.csv. No row was removed from the main fit.

A change in light travel time can cause timing curvature without orbital decay. Locally, timing acceleration and a true period derivative share the same quadratic form. Our timing-only model cannot separate them. The later spectroscopy study supplies independent observational evidence for that alternative, but we do not independently fit those spectra here. Our results neither confirm nor refute its binary solution.

Fixed offsets can also represent a persistent error in a fitted transit shape or timing procedure. We test this mathematical alternative. We have no evidence that such offsets occur at the required size. We do not inspect raw pixels, flux extraction, clocks, or changing transit shapes. Correct BJD conversion is assumed. There is no new raw instrument test.

The table spans different instruments at different epochs. That design lets offsets absorb much of the long-term curve. The two later instruments agree when tied to Kepler, but this agreement alone does not remove the offset sensitivity. Repeated observations with a stable instrument improve the constraint through changes within that instrument. This is the useful general method: report curvature after fitting group offsets, and show how the error changes with an explicit offset prior.

## Limitations

We use one historic table and its rounded errors. We do not add observations or establish a new phenomenon. The quoted times can share shape priors and other errors. Their covariance is not public in this table. A quadratic is a local description; it is not a physical orbital solution. Fixed offsets do not model time-varying systematics. The large null offsets and the independent binary evidence prevent an instrument-cause claim. We make no priority claim for the general use of group offsets in timing fits.

## Reproduction and provenance

Run from any folder:

    python /path/to/result/files/analyze.py

This reads the included timing CSV and writes the fit tables, prior grid, leave-one-out table, validation JSON, and static PNG next to the script. No network is needed. Tested with Python 3.12.16, NumPy 2.5.4, SciPy 1.18.1, pandas 3.0+ (exact used version in requirements.txt), and Matplotlib 3.11.2. The random seed is 1107.

The raw PDF is reused at the shared path ./datasets/kepler1658-vissapragada-2212.09752v1/paper.pdf. Its exact resolved path, source URL, byte count and SHA-256 are in files/provenance.json. The SHA-256 is db0a85813993a95e483e81fa31eb6955c5de5fa7effdeb7d5cf96d07fc7e2c7d. The helper retrieval command is also recorded there. We do not include the paper in this bundle.

To audit the transcription, install pypdf 7.0.0 in a private environment and run:

    python files/audit_source.py /path/to/shared/paper.pdf

The stored audit result is files/source_audit.txt. The numerical analysis does not need pypdf. Source tables remain attributed to Vissapragada et al.; the code and this analysis are new campaign outputs. The baseline license covers this package, not the source paper.

Job: sci-1107-dell-astronomy-7c8eaf62c254. Topic: astronomy. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-08 local time (2026-11-09 UTC). The signature uses a campaign-machine key. It is not a personal authorship claim.
