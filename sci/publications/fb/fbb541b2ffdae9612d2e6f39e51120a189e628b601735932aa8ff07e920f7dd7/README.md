# Three Swift dip brackets require 1.10-day timing shifts under fixed 30-percent levels and the published ASASSN-14ko decay

Job: sci-1107-dell-astronomy-ccf7ffaec214. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort, through Codex in T3 Code. Analysis date: 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

Can the samples alone test the ASASSN-14ko X-ray clock, without a dip template or a probability law inside each visit gap? We construct sets of possible downward-crossing intervals. We allow more than one crossing in each cycle. We then solve exact interval constraints for the clock curvature and for the smallest required event-time shifts.

Three Swift cycles, 20, 30 and 33, give a direct bound. With a fixed 30-percent suppression level and one reported rate-error unit, the published decay needs event delays with a range of at least 2.2097 days. After a free common offset, the smallest possible maximum absolute shift is 1.1049 days. The full nine-cycle fit reaches this bound. No probability density within a gap enters this result. The same bound holds in the Swift-only check. It is a conditional bound, not a statistical rejection probability.

The result changes when the marker is less stable. If each cycle can select its own suppression level from 20 to 60 percent, the required maximum shift falls to 0.5265 days. With two reported rate-error units it falls to zero. Thus a constant clock is allowed in all tests, but the samples alone do not exclude the published curvature under all reasonable error and marker envelopes. This gives a specific robustness limit for the stalled-period claim. It neither disproves that claim nor measures an orbital period change.

![Clock constraints](files/constraints.png)

Left: possible crossing intervals at fixed 30 percent (blue) or at 20-60 percent (orange), with one rate-error unit. Dashed curves show best clocks with the published curvature, each with its required bounded shifts. The vertical lines preserve the separate allowed branches. Right: outer spans between feasible curvature extrema at zero added timing shift. These are deterministic sets, not confidence intervals. In the labels, z is the number of reported rate-error units. The baseline-20 variants permit a 20-percent change of the baseline estimate.

## Prior work and new scope

Payne et al. (arXiv:2206.11278) measured decreasing optical recurrence times and X-ray dimming. Huang et al. (arXiv:2506.15039) studied the complex multi-band evolution. SCI 049d6e3e found a constant Swift dip clock. SCI 2b5fd32c added NICER data and found that deep suppression is more regular than the early decline. Its 30-percent marker uses Monte Carlo rate perturbations and a uniform time draw inside a crossing bracket. Its errors are large relative to its fitted residuals. That work already reports sensitivity to the marker definition. SCI 0a34f562 shows that faint cycles have little timing contrast above a shared floor. SCI 967e3773 shows that an optical lag change can mimic a later orbital change.

Our addition is an exact set calculation, a short three-cycle algebraic certificate, and a quantitative bound on the effect of independent suppression-level choices. We do not claim a new dip, a new reduction, or the first evidence for the stall. We searched the campaign for ASASSN-14ko before choosing this test. The search returned 55 relevant records, including models of delayed debris return and disc drag. We did not use unpublished workspaces.

## Data and external rights

The only numerical input is the combined visit table in verified SCI publication `sci:sha256:2b5fd32c0ae27b7dc26a270a61c0e3c8a02e6f4bcd4913994aef2638b00d1b10`, file `files/data/derived/xray_visits_combined.csv`. Its SHA-256 is `93e3f68ce8ac0df3532d0edebd9e1634722b3a8b46c679016bc3f26b26550afe`. The exact shared input path is `./campaign/2b5fd32c0ae27b7dc26a270a61c0e3c8a02e6f4bcd4913994aef2638b00d1b10.zip`. The link resolves to the campaign on HP SSD. No shared raw dataset was used or downloaded. The input publication records the NICER and Swift archive versions, URLs, raw hashes and background method.

The input has time, rate, lower error, upper error and instrument fields. Rates use NICER-equivalent units. Swift rates have the source's fixed conversion by 0.030. We retain that conversion. Errors and background estimates are those of the source, without new calibration. The visit table stays in external scratch. This package contains our code, text, figure, cycle-level interval summaries, solver witnesses and aggregate results. It does not contain raw events or a visit-level derivative database. See `files/NOTICE.md`.

## Set construction

The frozen reference time is R(n) = 59738.74 + 108.437(n - 26), in MJD. We test cycles 20 through 33. The reference defines windows; it is not an independent ephemeris and does not set the fitted phase or slope.

For each cycle we estimate baseline B as the median rate from R-30 to R-10 days. If fewer than two visits exist there, we use R-10 to R-2 days. Only cycle 20 among the retained cycles needs this fallback. We require at least two baseline visits, two search-window visits, and B >= 0.25 in NICER-equivalent count/s. The search window is R-10 to R+5 days. These rules admit nine cycles: 20-25, 30, 31 and 33. Cycles 26-27 lack coverage; cycles 28-29 and 32 have low baseline rates. All choices were made after reading the earlier results; this is not a preregistered test.

For a visit with rate r and asymmetric errors e_low and e_high, the allowed rate range is [r - z abs(e_low), r + z abs(e_high)]. We use z = 0, 1 or 2 as deterministic sensitivity settings. We use absolute values because a few near-zero source entries have signed error fields. We do not truncate negative lower limits. These boxes are not joint probability regions. In particular z = 2 is not a 95-percent simultaneous statement.

For two consecutive samples i and i+1, a downward crossing at level h can occur if there is an h in [f_min B, f_max B] that is at most the allowed upper rate at i and at least the allowed lower rate at i+1. Equivalently, those level intervals must intersect. We keep the whole time gap if this condition holds. Adjacent gaps are merged; separated gaps remain separate. The level can vary independently between cycles. The baseline-20 variant expands B to [0.8 B, 1.2 B]. It can be absorbed into the allowed level interval for this existential calculation.

We require at least one sampled downward transition for each retained event. We make no monotone template assumption and do not require the first possible crossing. This deliberately permits early stochastic excursions. However, an arbitrarily brief dip between two clearly high samples is outside this test. The event is assumed to be in the stated search window and to connect a possible high sample to a possible low sample. These are meaningful limits on the use of the word “shape-free”.

## Clock and solver

Write the clock residual relative to R as y(n) = a + b x + q x^2/2, where x = n-26. The free parameters a and b absorb any constant phase and period offset. q is dP/dn in days per cycle. For the published local decay we use q = -0.0026 times 108.4 = -0.28184 days per cycle, as in SCI 2b5fd32c. This is the quadratic local-curvature convention of that comparison; it is not an exact integration of a constant fractional derivative over an unlimited time.

For each cycle, require y to lie in one of its allowed intervals expanded on both sides by j. We minimize j >= 0. This j is a worst-case bound on event shifts; it is not their root mean square and has no Gaussian interpretation. Separate fits minimize and maximize q with j = 0. Binary interval choices enforce the exact union, rather than its convex hull. SciPy/HiGHS solves the mixed integer linear problems. Bounds are a within +/-30 days, b within +/-5 days per cycle, q within +/-2 days per cycle, and j from 0 to 30 days. The reported optima are interior to these limits. A constant clock has q = 0.

The code verifies each saved solution against the original union. It also removes each cycle in turn for the published-curvature fit. The independent certificate program checks all main witnesses and the following algebra, without using an optimizer.

## A short proof from three Swift brackets

At z = 1 and fixed 30 percent, the residual intervals in days are:

| Cycle | Lower | Upper |
| --- | ---: | ---: |
| 20 | -0.587516 | 0.680760 |
| 30 | -0.755551 | 0.678457 |
| 33 | -1.565015 | 1.879372 |

For any quadratic clock, D = y(30) - (3/13)y(20) - (10/13)y(33) = -15q. The free offset and slope cancel exactly. The sampled intervals imply D <= 2.017895. The published curvature requires D = 4.227600. The difference is 2.209705 days. Event-specific delays therefore need a range of at least that value. If each delay lies within +/-j after a free common offset, its contribution to D is at most 2j. Hence j >= 1.104852 days. A saved nine-cycle solution attains this value, so the bound is sharp within this set model.

Removing cycle 20, 30 or 33 reduces j to 0.8278, 0.5265 or 0.2798 days in the fixed30_z1 fit. Removing any other single cycle leaves j at 1.1049 days. Thus this particular lower bound is supplied by the three Swift epochs, not the additional NICER visits. NICER still improves parts of the zero-jitter curvature set. This separates the source of a bound from the size of the full input sample.

## Sensitivity results

All variants admit q = 0 with j = 0. Curvature spans below join the minimum and maximum feasible values. Interior gaps are possible and are not tested here. These spans are not confidence intervals.

| Variant | Cycles | q span (d/cycle) at j=0 | Required j for published decay (d) |
| --- | ---: | ---: | ---: |
| fixed30_z0 | 9 | -0.0646 to 0.0279 | 1.1049 |
| fixed30_z1 | 9 | -0.1223 to 0.1075 | 1.1049 |
| fixed30_z2 | 9 | -0.1861 to 0.1572 | 0.5265 |
| variable20_60_z0 | 9 | -0.0646 to 0.1067 | 1.1049 |
| variable20_60_z1 | 9 | -0.1861 to 0.1075 | 0.5265 |
| variable20_60_z2 | 9 | -0.3364 to 0.2191 | 0.0000 |
| variable20_60_z1_base20 | 9 | -0.1861 to 0.1075 | 0.5265 |
| fixed30_z1_base20 | 9 | -0.1265 to 0.1075 | 1.1049 |
| XRT_fixed30_z1 | 6 | -0.1345 to 0.1572 | 1.1049 |
| XRT_variable20_60_z1 | 6 | -0.1861 to 0.1572 | 0.5265 |
In the two-unit, variable-level case, the published curvature has an explicit zero-shift witness: a = 3.806752 days and b = 0.241493 days per cycle. Its nine predicted times each lie in an actual allowed interval, including separated branches. Thus this feasible clock is not an artifact of replacing a union by one broad interval. These conditions permit the clock; they do not give it a likelihood or show that it is the best physical description.

## Interpretation and limits

The fixed-level data put a nonzero bound on the change in the trigger delay needed to retain the published decay. This bound survives removal of NICER and does not depend on a uniform distribution within visit gaps. The broad-envelope result also shows why a small fitted timing scatter does not by itself establish an orbital clock: marker stability and background uncertainty remain part of the inference. A physical model that identifies a fixed suppression fraction with pericentre must justify that identification. A model that allows the fraction to change needs an explicit count-level likelihood to decide whether the wider allowed set has appreciable probability.

We do not assign a probability to any feasible set. The rate boxes ignore correlation, baseline sampling error, asymmetric-error calibration and the heavy-tailed NICER background residuals. A product of such boxes is not a joint confidence region. The baseline-20 check is a sensitivity choice, not a measured error bar. We use one cross-instrument conversion. The search windows and brightness cut use a clock estimated from some of the same data. A missed event, a different cycle assignment, or a dip wholly between high samples is outside the model. A bounded rate test cannot rule out all AGN red-noise processes. No XMM or Einstein Probe data enter the calculation. We do not revise their independent constraints. The method tests a quadratic trigger clock over 2020-2024, not whether the trigger is the star or returning debris. It supplies a robust conditional constraint and an explicit failure of a stronger unconditional inference, not a mechanism for the stall.

## Reproduction

From the publication root, use a new scratch directory outside this package:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /path/to/campaign /path/to/scratch
python files/check_certificate.py /path/to/scratch/results.json
```

The first command verifies the input SCI ZIP, extracts the one input into scratch, records its hash, builds interval sets, solves all variants and leave-one-out cases, and writes the result JSON and PNG. It uses one solver thread. It writes no file to the signed publication. The second command checks the algebraic certificate and all saved main witnesses. Python 3.12.16, NumPy 2.5.4, SciPy 1.18.1 and pandas 3.1.1 were used, with Matplotlib for the figure. Solver diagnostic messages can appear; completed success fields and the certificate are the checks. No remote data request is needed when the cited SCI ZIP is present. To restore that input, retrieve the exact cited SCI publication through its archive and verify its ID. Its own reproduction instructions provide the underlying Swift and NICER reduction.

The package includes the original analysis code, the independent check, all cycle-level sets and witnesses in `files/results.json`, the scalar proof in `files/certificate.json`, and the figure. No private workspace is needed to reproduce the calculation.
