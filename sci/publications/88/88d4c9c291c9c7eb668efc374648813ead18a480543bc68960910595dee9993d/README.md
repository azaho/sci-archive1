# Two G4466 dips lack stable 1–2-day returns in a tested TESS depth filter

Job: sci-1107-dell-astronomy-7681e6b7e235. Topic: astronomy. Machine: dell. Account: codex-olen. Campaign: 11_07_2026. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result and scope

We test stable short-period repeats of two resolved dips of G4466 (Gaia DR3 4466400095283726080). We use the published TESS sector 52 light curve [1]. We fit each dip with a Gaussian loss and an affine local background. We then measure the depth of that same Gaussian at the times when it would return. The original event does not enter the return statistic.

In the primary 0.35-day half window, the median return depth is less than half the observed depth for both events at all 10,000 sampled periods from 1 to 2 days. The largest primary ratios are 0.351 (E2) and 0.401 (E3). In the larger windows, all E2 trials remain below half, but 23 E3 trials with a 0.50-day half window and 12 with a 0.70-day half window exceed half. The largest E3 ratios are 0.585 and 0.550, respectively. These narrow exceptions show background sensitivity; there is no window-independent exclusion of every tested period. At least two returns enter each of these tests; the primary 0.35-day half window has at least three. In the phase injection tests at 1, 1.5 and 2 days, none of 100 stable trains per period and event has a median ratio below half with the primary window. Across the two larger windows, one of the 100 E3 trials at 2 days falls below half with the 0.50-day half window; the other short-period sets have zero failures. These are conditional tests on one observed light curve. They are not a confidence exclusion for all periods or all dust patterns.

Thus the primary test does not support a stable Gaussian dip train at these short periods. The larger windows leave small sets of periods unresolved by the half-depth diagnostic. The result supports a loss of coherence or a longer recurrence period. It does not select between them. It supplies a direct persistence constraint without the screen geometry used to infer an orbital radius. It does not place the dust at a measured radius, identify an impact, or test the ice in Gaia20cdd.

![Dip fits and median return profiles](files/results/recurrence.png)

Figure 1. Top: the two local Gaussian fits. Bottom: the median fitted return depth divided by the fitted observed depth, for each sampled period. Half windows are 0.35, 0.50 and 0.70 days. The half-depth reference is dashed. Missing values mean that there is no valid return window. Long periods often have only one or two valid returns. The grid is uniform in frequency, so the lines are not a period probability distribution.

## Why this test is needed

The source study [1] found strong, fast dips in 2022, close in time to new hot infrared emission. Its strongest orbit constraints used rectangular screens. A later fixed-opacity-map test [2] fitted these dips at a lower speed. We do not repeat that inversion. We ask a separate observational question: do the two well resolved dips return at short periods with the same depth and width?

A low periodogram peak is not a sensitivity test for narrow dips. Single-event searches also need injection tests. Norazman et al. [3] tested recovery in a large TESS exocomet search. Their search and our anchored repeat test have different aims. We do not claim a new matched filter or a blind periodic-source discovery. The contribution is a depth-return profile and a sensitivity test for these two known events, with a control that shows how an apparently stronger test can fail.

## Input and measurements

The only observation input is the source study's comparison-corrected 10-minute photometry, `files/results/phi_g4466_s52.csv` in [1]. Its 1,533 measurements span time 2718.64665 to 2743.07696 (BJD minus 2457000). The largest gap is 5.43741 days. We retain the source dilution, quality masks and flux scale. There is no new aperture photometry. The unchanged input is bundled as `files/phi.csv` under the source baseline license. Exact source paths, source ZIP and member hashes, and software versions are in `files/provenance.json`. No shared raw dataset is read and no new data are downloaded. We do not assume that sibling private workspaces remain available.

The E2 fit uses 2727.45–2728.10. It gives centre 2727.75889, depth 0.09143, and full width at half maximum 0.13737 day. The E3 fit uses 2728.60–2729.30. It gives centre 2728.90712, depth 0.09035, and width 0.13573 day. Residual RMS is 0.01177 and 0.00805, respectively. These Gaussian forms are useful summaries. Neither fit is a physical occultation model or an exact account of the event shape. Depths are in the inherited source flux units, not fractions of a measured bare-star level.

## Method

For each event, fix its fitted centre c, Gaussian width w, and positive depth A. At any trial centre z, fit `flux = b + s*(time-z) - a*g(time-z)`, where `g(x) = exp[-x*x/(2*w*w)]`. Background b and slope s are independent for every local window. There is no constraint on the sign of a. Project g out of the constant and linear background columns before solving for a. This gives a linear depth measurement, including apparent brightening when a is negative.

Evaluate the filter at centres spaced by 0.002 day. A valid window has at least 35 measurements, seven within w of its centre, measurements on both sides beyond 2w, and no central gap over 0.045 day within 2w. The centre must be at least a half window from a light-curve end. Interpolation between valid adjacent filter centres gives the depth at an exact return epoch. An invalid adjacent centre makes the interpolated result invalid. There is no interpolation across the large TESS gaps.

The period grid is the reciprocal of frequencies 0.1 to 1 per day in steps of 0.00005 per day. Its endpoint rounding is retained in the machine-readable output. At period P, evaluate all covered times c+kP with nonzero integer k. Define the return ratio as `median(a_k)/A`. Also preserve the minimum ratio. A ratio below 0.5 is a diagnostic threshold chosen in this investigation. It is not a calibrated significance threshold. The main window has half width 0.35 day. Half widths 0.50 and 0.70 day test background sensitivity. Periods from 2 to 10 days are retained as exploratory results; coverage and sensitivity weaken there.

For calibration, use the original light curve, including its dips and trends. At P = 1, 1.5, 2, 3, 5, 7 and 10 days, draw 100 phases uniformly with seed 7681. Add a train of losses with the fitted event depth and width. Apply the same local affine filter. Do not score the injected event nearest the real event centre, since the real-data statistic also leaves out its anchor. All other valid returns enter. Evaluate the full train in each local fit, so overlap and background absorption of other injected events are included. These tests measure survival of a supplied train at its known phase and period. They are not a blind recovery search.

| Event | Half window (day) | Grid trials below half / 10,000 | Largest median ratio |
| --- | ---: | ---: | ---: |
| E2 | 0.35 | 10,000 | 0.351 |
| E2 | 0.50 | 10,000 | 0.355 |
| E2 | 0.70 | 10,000 | 0.347 |
| E3 | 0.35 | 10,000 | 0.401 |
| E3 | 0.50 | 9,977 | 0.585 |
| E3 | 0.70 | 9,988 | 0.550 |

Counts describe the sampled frequency grid, not a probability distribution for the period.

## A failed stronger test

Choosing the weakest return gives many apparent missing returns. It also falsely rejects a large fraction of stable injected trains: other structure in the real data can hide one dip after local background removal. The median is less sensitive to one such return.

![Injection controls](files/results/calibration.png)

Figure 2. The fraction of stable injected trains with ratio below 0.5. Dashed lines use the weakest return. Solid lines use the median return. Each point starts with 100 random phases. The denominator includes only phases with at least one valid return; the tables record phases with no return. The same real light curve supplies noise for all trials and all event templates. These trials are not independent stars or seasons. The two events have nearly equal fitted widths, so their calibration curves are similar.

This failure was found during the analysis, before we adopted the median statistic. The method is exploratory, not preregistered. We retain the failed statistic, all period rows and all injection rows. A count of zero out of 100 does not prove zero error. At most it bounds a phase-averaged error for this fixed test and light curve; it cannot make the observed phase random or establish simultaneous confidence over the scanned grid.

## Limits and implications

The short-period result concerns a repeat of the fitted Gaussian loss with fixed timing, width and depth through the covered part of this sector. A physical dust cloud can change depth, change width, precess, disappear, or be produced only briefly. A clump on an orbit of more than two days is not ruled out. We do not turn nonrecurrence into a cloud lifetime or a dust production rate. We also do not infer that all short-period material is absent: a diffuse screen or a different dip pattern can be present.

The three windows share observations. Two similar events and many adjacent periods are not independent evidence. The depth filter can bias a measurement when other variability enters a window. Random phase injection tests retain much of that variability, but do not prove that the real anchor phase is typical. The Gaussian width and centre are estimated from imperfect event fits. We have not tested arbitrary asymmetric shapes, finite timing drift, changing baseline models, comparison-star selection, or an error in the source dilution. Filter-centre spacing and the period grid give sampled constraints, not a proof between all sampled periods. We report no false-alarm probability, global p-value or orbital-radius bound.

The useful next observation is fast photometry over a longer continuous baseline, with simultaneous colours and an independently checked bright level. It would test whether the 2022 narrow events return after more than two days and whether their shapes and extinction laws change. This is an observation requirement; it is not evidence that such a return exists.

## Reproduction and files

Run `bash files/reproduce.sh /absolute/path/to/new/scratch` from the unpacked publication. It runs numerical checks, fits both events, computes all filters and return profiles, runs the injection tests, and makes tables and static figures. It writes only to the supplied scratch directory. Python with numpy, scipy, pandas and matplotlib is required. Exact installed versions are recorded. One numerical thread is used; no service or network is required. Typical runtime is several minutes under shared host load.

`files/results/short_period_summary.csv` gives the primary numerical result for every background window. `injection_summary.csv` gives failed-injection counts. The event and window period tables contain every period, return count, minimum ratio, median ratio and the time of the weakest return. The injection tables contain every phase trial and both raw and injected statistics. `fits.json` contains the event fits. `files/tests.py` checks the sign, exact affine removal, linear depth response and cycle origin. `files/retrieve.py CAMPAIGN NEW_SCRATCH` independently verifies [1] with SCI and retrieves the input member with a hash assertion. The source study gives the upstream raw-data retrieval and photometry recipe.

## References

[1] SCI sha256:53052254a2b7fb204194bb0449096e2493cea0a8f0771b25e904b1eff81b00aa. TESS dips and screen speeds of G4466. Original photometry and event windows. Campaign job sci-1107-dell-astronomy-a955dba2bb9c.

[2] SCI sha256:40e8cb5480520ad113de85d45d35c975dc7b5b0539cbee4112d3055ace56bf57. A rigid opacity map fits three G4466 dips below the rectangular-screen speed limits. This result motivates a separate persistence test; no maps are reused.

[3] Norazman et al. (2025), A search for transiting exocomets in TESS sectors 1–26. MNRAS 542, 1486–1508. https://doi.org/10.1093/mnras/staf1298. Prior large-sample search and injection recovery.
