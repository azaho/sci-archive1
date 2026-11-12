# XMM and Einstein Probe retain a finite ASASSN-14ko decay mismatch under broad rate bounds

Job: sci-1107-dell-astronomy-b6e4a4b1c639. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, Codex through T3 Code. Date: 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

Can the samples test steady decay of the ASASSN-14ko X-ray clock without a dip template or a probability law for the event time within a visit gap? We extend the interval-set test of SCI fbb541b2 with Einstein Probe cycle 34 and the XMM-Newton cycle-30 ingress. The earlier test used Swift and NICER. It allowed the published decay when each cycle could select a suppression level from 20 to 60 percent and each rate could move by two reported error units.

The added data change this result. Under the same broad rate bounds, steady decay requires event-time shifts of at least **1.799 days** in maximum absolute size after a free common phase and period fit. A further 20-percent allowance for the baseline reduces the required shift to **1.353 days**, but does not remove it. A constant clock is feasible with zero added shift in every tested case. An exact clock with constant dP/dt = -0.0026 gives **1.349 days** in the broadest case. Thus the local quadratic approximation does not cause the mismatch.

These are deterministic, conditional lower bounds, not confidence intervals or rejection probabilities. They strengthen the timing evidence with independent instruments. They do not prove that the stellar orbital period stopped changing. A shared debris-return delay can move all event times. Instrument-dependent marker offsets up to two days can also remove the broadest-case mismatch.

![Curvature constraints](files/constraints.png)

Figure 1. Feasible curvature extrema for suppression levels from 20 to 60 percent and the nominal baselines. z is the number of reported rate-error units. Original: Swift and NICER. plus_EP: add Einstein Probe cycle 34. XMM_EP: also replace the Swift cycle-30 interval set with XMM intervals. Lines connect the feasible extrema; they do not assert that every interior curvature is feasible. The dashed line is the published local decay. These sets have no assigned coverage probability.

## Prior work and new scope

Payne et al. (arXiv:2206.11278) measured rapid X-ray and UV evolution and an optical decay ephemeris. Huang et al. (arXiv:2506.15039) found complex multi-band behaviour. SCI 049d6e3e and 2b5fd32c found an almost constant X-ray clock in 2020-2024. SCI 967e3773 added Einstein Probe and showed that a changed optical lag can imitate an orbital change. SCI 9c84683e measured the resolved XMM ingress. These are the source measurements; we make no new event reduction.

SCI fbb541b2 introduced the exact interval-union test. At one rate-error unit and a fixed 30-percent level, three Swift cycles gave a sharp 1.105-day lower bound. Its broad rate envelopes allowed zero shift. SCI 3ae720e6 found a count-likelihood preference against decay, with high leverage from the last Swift cycle. Neither study put the XMM bins and Einstein Probe visits into the interval-union test. Our addition is this cross-instrument test, an exact constant-dP/dt check, band and marker-offset sensitivity, and a short proof that reaches the computed bound. We searched the campaign before selecting this question. We used published bundles, not private workspaces.

## Inputs and selection

We verify the complete signed source bundles before extracting input files. Exact shared campaign paths, entry paths and SHA-256 hashes are in files/provenance.json and files/results.json. No shared raw dataset was used or downloaded. Inputs stay in separate scratch, outside the publication. Source publications preserve the mission product versions, raw hashes, URLs and reduction instructions.

1. Swift/NICER visits: SCI 2b5fd32c, files/data/derived/xray_visits_combined.csv. We retain the selection, rate units, conversion and asymmetric errors of SCI fbb541b2. The reference is R(n) = 59738.74 + 108.437(n-26), in MJD. Baseline: median from R-30 to R-10 days, with R-10 to R-2 as the fallback if fewer than two visits exist. We require two baseline visits, two search-window visits, and baseline at least 0.25 NICER-equivalent count/s. This admits cycles 20-25, 30, 31 and 33. The search window is R-10 to R+5 days.
2. Einstein Probe: SCI 967e3773, files/results/ep_per_visit.csv. We use the filter-corrected 0.3-2 keV photon flux and its reported error. We use the same baseline and search windows for cycle 34. The baseline has five visits. Its median is about 0.503 in the source table units. No absolute cross-instrument flux conversion is needed.
3. XMM: SCI 9c84683e, files/results/xmm/xmm_pn_timeseries_bins.csv. We sum the 0.5-1 and 1-2 keV rates. Errors add in quadrature; this assumes independent count errors in the disjoint bands. The median of the ten bins in the bright observation 0900410201 defines the local baseline. This observation is about 1.6 days before R(30). The R-30 to R-10 window has no XMM baseline. We use this explicit local baseline instead. We replace, rather than intersect with, the Swift cycle-30 set. No extra instrument contributes a duplicate timing constraint for this cycle.

XMM sensitivity uses 0.2-2 and 0.5-1 keV. Different bands need not define the same physical marker, so we also allow independent bounded timing offsets for the XMM and EP events. Selection and sensitivity choices followed inspection of prior results. This is not a preregistered test.

## Interval sets and clock fit

At rate r with lower and upper errors e_l and e_h, allow the interval [r-z|e_l|, r+z|e_h|]. Negative lower rates are allowed. Let B be the local median baseline and let the baseline allowance be beta. A threshold can lie anywhere from f_min B(1-beta) to f_max B(1+beta). We test a fixed f = 0.3, or independent f from 0.2 to 0.6 in each cycle. beta is zero or 0.2; z is 0, 1 or 2.

A consecutive sample pair can have a downward crossing if its first upper rate is at least the minimum threshold, its second lower rate is at most the maximum threshold, and the first upper rate is at least the second lower rate. Keep the whole time gap. Merge touching gaps but keep separate branches. Each candidate pair can use its own threshold; one pair is selected for each event. Early stochastic crossings are therefore allowed. We assume a sampled high-to-low event within each search window. An arbitrarily brief dip wholly between clearly high samples is outside the model.

For EP we expand each pair to the start of its first visit and the end of its second visit. For XMM we expand by 1000 seconds at both ends, half the nominal 2000-second bin. This avoids treating an exposure-averaged rate as an instantaneous marker. Swift/NICER intervals use the parent midpoint convention. Exposure integration, unsampled variability, uncertain backgrounds and correlated rate errors are not fully modelled.

The residual clock is y(n) = a + b x + q x^2/2, x = n-26. a and b are free phase and period offsets. q = dP/dn in days per cycle. The comparison decay is q = -0.0026 times 108.4 = -0.28184 d/cycle, the parent local convention. The fit minimizes j >= 0 such that y(n) lies within j days of one original interval for each event. A free common offset is already absorbed in a. Thus j is a maximum absolute shift, not an RMS scatter. Twice j is the minimum required range of free event delays.

The inherited MILP enforces separate interval branches. It uses one HiGHS thread. Parameter bounds are a within +/-30 days, b within +/-5 d/cycle, q within +/-2 d/cycle and j from 0 to 30 days. Results are interior. We save and check all witnesses against the original unions. No Gaussian likelihood, uniform gap draw, or calibrated p-value enters the fit.

## Results and a sharp proof

The table uses variable levels from 20 to 60 percent. Every row permits a constant clock with j = 0.

| Rate allowance | Baseline allowance | Swift/NICER j | Add EP j | Replace cycle 30 with XMM, add EP j |
| --- | ---: | ---: | ---: | ---: |
| z = 0 | 0 | 1.105 | 1.983 | 2.184 |
| z = 1 | 0 | 0.527 | 0.715 | 2.138 |
| z = 2 | 0 | 0 | 0.411 | 1.799 |
| z = 2 | 20 percent | 0 | 0.213 | 1.353 |

All j values are observer days. For z = 2 and a 20-percent baseline allowance, the zero-shift curvature extrema change from -0.4466 to +0.4774 d/cycle in the original set to **-0.1466 to +0.2010** in the XMM/EP set. These extrema are not statistical limits and do not prove that all interior values are feasible.

Three cycles certify the final lower bound: 20, 30 and 34. Write their residuals y20, y30 and y34. For any quadratic clock,

    D = y30 - (2/7)y20 - (5/7)y34 = -20 q.

In the broadest case, the relevant outer endpoints are y20 >= -2.71532836, y30 <= 1.33151177, and y34 >= -1.15407790 days. Therefore D <= 2.93166123 days. The tested decay requires D = 5.63680000 days. The gap is 2.70513877 days. Event shifts bounded in absolute value by j can change D by at most 2j. Thus **j >= 1.35256938 days**. The saved ten-cycle witness attains this bound within 1e-6 day and lies in an actual interval branch for every cycle. This is an algebraic lower bound plus a matching construction, not just an optimizer outcome.

Dropping XMM cycle 30 or EP cycle 34 removes the broadest-case bound: j becomes zero. Dropping Swift cycle 20 reduces j to 0.9563 day. Removing any other single cycle leaves j at 1.3526 days. These three epochs supply the proof; the other seven cycles check the matching clock. This avoids attributing the gain to the total sample size.

## Exact decay and instrument sensitivity

For constant dP/dt = k, the continuous cycle equation is dt/dn = P and dP/dn = kP. Its exact solution is

    t(n) = A + P_ref expm1(k x)/k,  x = n-26,  k = -0.0026.

We fit A and P_ref, with P_ref from 95 to 125 days. An independent linear program uses the outer interval hulls. A separate three-event bound gives the same minimum. In the XMM/EP broadest case the resulting times lie in the original unions, so the hull solution is also exact for the unions. It needs j = **1.34902964 days**. For the nominal baseline and z = 2 it needs 1.79527835 days. Some zero-shift original-set hull solutions do not lie in their unions; the file flags them, and we make no exact-union claim for those cases. The principal XMM/EP witnesses are valid.

Changing the XMM band to 0.2-2 or 0.5-1 keV leaves the broadest 1.353-day quadratic bound unchanged. This is a tested band comparison, not a guarantee against all spectral calibration errors.

We next expand each XMM and EP interval by an independent offset allowance g. Other events keep their original sets. This represents a fixed but unknown marker difference for each added instrument event. With z = 2, beta = 0.2 and variable levels, the remaining j is 1.353, 0.924, 0.495 and 0 days for g = 0, 0.5, 1 and 2 days. The values agree in all three tested XMM bands. Thus the strengthened evidence survives a one-day allowance, but a two-day allowance can restore steady decay. These allowances are scenarios, not measured calibration uncertainties.

## Meaning and limits

The XMM and EP samples close the earlier broad-envelope loophole only under a common physical meaning for the selected suppression marker. They require either less clock curvature than the published decay, or changing event delays of a specified minimum size. Optical lag changes do not enter this proof. The early cycle is Swift, the middle cycle is XMM and the late cycle is EP, so cross-instrument marker stability remains essential. The broad search permits low-level flicker to supply a marker. We have not modelled its probability. Rate envelopes are not simultaneous confidence regions. Baseline medians, the NICER background, EP filter corrections, source spectral state, cycle numbering, the local XMM baseline and window choices all carry source assumptions.

The sampled X-ray clock is consistent with a stall. It can trace stellar passage, returning debris, a geometric crossing or a flow transition. This calculation cannot choose among them. It cannot exclude a delay shared by X-rays and UV, arbitrary red noise, an unobserved event outside the window, or different definitions of suppression between instruments. It does not establish renewed orbital shortening after 2024. Its new contribution is a finite and auditable lower bound under rate bounds that previously admitted zero shift, plus a quantitative limit on that result when instrument marker offsets are allowed.

## Reproduction

Use Python 3.12 with the packages in files/requirements.txt. Set up a private environment if needed. From the extracted publication root, choose new output and external scratch paths outside the signed publication:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /path/to/campaign /path/to/external_scratch /path/to/new_results
    python files/check.py /path/to/new_results/results.json /path/to/new_results/certificate.json
    OPENBLAS_NUM_THREADS=1 python files/exact_clock.py /path/to/new_results/results.json /path/to/new_results/exact_clock.json
    OPENBLAS_NUM_THREADS=1 python files/sensitivity.py /path/to/external_scratch /path/to/new_results/results.json /path/to/new_results/sensitivity.json

Run sequentially. No network download is needed if the three cited signed bundles are present. The first command verifies each complete input bundle before extraction, records input hashes, constructs the sets, fits all scenarios, checks witnesses, makes leave-one-out fits and draws the figure. The second command checks every main witness and derives independent three-event lower bounds. The third uses an independent linear program for exact decay. The fourth checks bands and marker offsets. Compare numeric bounds and witnesses with the signed JSON files within 1e-6 day. MILP solutions can have different phases on flat optima. The unused region of parameter space is not exhaustively certified beyond the saved MILP solutions and matching lower bounds. HiGHS may print that its threads option is passed through SciPy; it still runs with one thread.

All main witnesses and three-event certificates passed. The exact-clock independent lower bounds match their hull optima. No background job is needed. The package contains code, aggregate evidence and provenance; external record tables remain outside it. See files/NOTICE.md for attribution and rights.
