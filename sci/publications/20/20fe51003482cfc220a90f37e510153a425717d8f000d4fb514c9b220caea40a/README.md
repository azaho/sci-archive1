# Three serial filters leave ocean damping unresolved in an SST-only model

## Result and scope

A correction of SST input steps does not, by itself, identify the ocean damping time. We prove this result for a daily linear model with three serial first-order filters. The filters represent persistent forcing, ocean response, and analysis smoothing. All six assignments of three distinct time constants give exactly the same SST output. This includes the full spectrum, all lag correlations, and all event statistics computed from that output. Comparisons among SST products do not remove a common-factor ambiguity. An unfiltered buoy can remove the analysis factor, but it does not separate forcing persistence from ocean damping.

This is a method study with original synthetic data. We do not fit this model to DOISST, estimate a new SST correction, or infer an actual ocean damping trend. We give an exact set of permitted damping changes, a tool to calculate that set under stated bounds, and a two-proxy moment method that identifies damping under stronger measurement assumptions. The latter method is exact in population. Its sampling uncertainty is large in our noisy 44-year test. Its failure under shared proxy error or a filtered buoy is part of the result.

## Prior work and the added result

The selected campaign study, [SCI f50dc28f](sci:sha256:f50dc28f2fb7a9fc7ae32b687b845a53ebf24145c750d16d7526fb3b01221f28), found that a loss of fast variance accounts for most of the increase in one-lag SST memory in DOISST. It fit a separate amplitude and decay time to correlations at lags 5 to 20 days. It allowed that the decay time could still reflect real change. The [16-member correction study](sci:sha256:e2e438dd3d5117f2238bb0b082b06daea99406355e30019bf8c3e33714fac3b3) showed that correction choice changes several event trends. We ask what physical attribution remains possible after such corrections.

The basic stochastic SST model dates to [Frankignoul and Hasselmann (1977)](https://doi.org/10.1111/j.2153-3490.1977.tb00740.x). [Lee et al. (2025)](https://doi.org/10.1038/s41558-025-02245-w) used daily SST persistence to study thermal inertia. [Li et al. (2025)](https://doi.org/10.1007/s00382-025-07884-5) showed that atmospheric forcing has substantial memory. A two-factor ambiguity is already explicit in [Kwasniok (2024), section IV B, equations 47-48](https://doi.org/10.1063/5.0170130): linear damping and colored-noise decay can exchange roles. We do not claim that two-factor result as new. The additions here are the three-factor daily SST construction, exact change sets under external bounds, the limit of joint SST-product comparisons, and a two-proxy design with explicit failure tests. These are a focused extension, not a new general system-identification theory.

## Model and proof

Let L denote a one-day delay. Define a stable filter

    H_p(L) = (1-p)/(1-p L),    0 < p < 1,
    tau = -1/log(p) days.

Let e be an independent unit-variance driving sequence. Use

    F = H_b e,
    X = H_a F,
    Y = H_c X.

X is true SST, F is an external forcing index, and Y is analysed SST. The ocean equation is X_t = a X_(t-1) + (1-a) F_t. The index F is not a measured heat flux in this construction. All means are zero. Gains can be absorbed in forcing amplitude. We exclude extra zeros, feedback, advection and seasonal coefficients from this tested model.

**Proposition 1.** The transfer from e to Y is

    K(L) = (1-a)(1-b)(1-c) / [(1-aL)(1-bL)(1-cL)].

Multiplication of scalar filters commutes. Thus every permutation of a, b and c has the same transfer, path by path, for the same e and consistent zero initial conditions. The result also holds for stationary solutions obtained by driving from the infinite past. No Gaussian assumption is needed. With a common added observation-noise process, equality is retained. For Gaussian driving, the entire output probability law and every finite-record likelihood are identical. No statistic of Y can label the three factors. Under the exact three-factor, distinct-positive-pole model, the three roots are identifiable in an ideal infinite record; their physical labels are not. Unknown zeros, noise, or a different model can make even root recovery uncertain.

**Corollary.** Removing an additive fast-noise component does not establish which remaining pole is ocean damping. Fitting an amplitude times one exponential at positive lags also does not establish this. In the generic positive serial-filter model the slowest pole sets the asymptotic correlation tail, irrespective of its physical label. At finite lags several poles contribute. This differs from the additive two-variance model used in the prior campaign fit.

**Proposition 2.** Suppose products have outputs Y_i = G_i H_c H_a H_b e, with arbitrary fixed stable scalar product-specific filters G_i. The same permutation leaves every Y_i unchanged at once. Thus all their cross spectra, cross correlations and joint Gaussian likelihoods remain unchanged. More products can constrain relative responses G_i/G_j; they cannot in general label a common hidden factor. Even if c is known and removed in all products, exchange of a and b remains possible. A buoy B = X + measurement error with known unfiltered response removes the ambiguity involving c, but leaves that two-factor exchange.

Both propositions concern constant coefficients within a record or separate stationary periods. We do not assert equality through a known switch with prescribed continuous hidden states. A resolved switch transient, known input response, independent forcing measurement, or nonlinear dynamics can supply information that this model lacks. Agreement among products that have known independent responses can also impose additional restrictions.

## Exact numerical example and permitted changes

All numbers below are synthetic. Early time constants are {1, 3, 20} days. Late constants are {3, 8, 20} days. In the reference assignment the ocean stays at 20 days, forcing stays at 3 days, and the analysis filter changes from 1 to 8 days. The forcing amplitude and the driving sequence are held fixed.

The population one-lag metric -10/log(rho_10) rises from 29.73 to 58.34 days. A least-squares amplitude-times-exponential fit at lags 5 to 20 rises from 21.13 to 30.97 days. Both rises occur with an unchanged 20-day ocean response. This example does not seek to match the size or spectrum of any observed SST step.

There are six labels in each period and 36 pairs of labels. Permitted ratios of late to early ocean time range from 0.15 to 20. If forcing must have the same time constant in both periods, eight pairs remain, and the ratio range is 0.4 to 20. These are discrete identified sets with extrema, not continuous confidence intervals or equally likely alternatives. For example, all three histories below retain a 3-day forcing time and identical analysed SST in each period:

| Ocean time, early to late | Analysis time, early to late | Interpretation |
|---|---|---|
| 20 to 20 days | 1 to 8 days | No ocean change |
| 1 to 20 days | 20 to 8 days | Ocean time increases |
| 20 to 8 days | 1 to 20 days | Ocean time decreases |

External bounds can resolve the labels. If both forcing and analysis times are known to be no more than 8 days in both periods, the 20-day root must be ocean damping, and its change ratio is 1. With bounds of 2 days for both non-ocean factors, no assignment is possible: those bounds contradict this exact model and these roots. In general, a single pole above both non-ocean bounds must be the ocean pole if at least one complete assignment exists. Two such poles rule out the assumed model. This rule is implemented by full enumeration in `files/label_poles.py`. Bounds must come from external evidence. They are not justified by the SST fit itself.

## A measurement design that resolves the ocean factor

Consider an unfiltered buoy B_t = X_t + eta_t and two forcing proxies Q1_t = F_t + u_t and Q2_t = F_t + v_t. Suppose

    X_t = r X_(t-1) + g F_t.

The forcing may be colored. Assume stationary finite moments, measurement errors independent of the true forcing and state, and each measurement-error process independent of the others at all lags. Let Z_t be the column vector (Q2_t, Q2_(t-1)). Then

    E[Z_t B_t] = E[Z_t (B_(t-1), Q1_t)] (r, g)^T.

Proof: substitute B and Q1. The residual is eta_t - r eta_(t-1) - g u_t. Each term has zero cross moment with Z by the stated independence. If the 2 by 2 moment matrix has full rank, inversion uniquely gives r and g. This is a standard instrumental-variable construction applied to this measurement problem; no general novelty of instrumental variables is claimed. It does not need white forcing or known noise variances. Forcing proxies must measure the same exogenous forcing. A net surface heat flux that contains SST feedback does not automatically meet this requirement. Two reanalysis flux fields that share observations or model errors do not automatically give independent proxies.

`files/audit.py` checks these population moments by a separate impulse-sum method. It recovers r = 0.9512294245 and g = 0.0487705755, which give a 20-day ocean time. In the 200 finite-record tests, each record has 16,060 daily values after a 2,000-day burn-in. Forcing time is 3 days. Each proxy has independent white error with standard deviation equal to the forcing standard deviation; buoy error is 0.3 times the SST standard deviation. The median r is 0.9537; the central 95% simulation range is 0.9028 to 1.0020. Seven of 200 estimates lie outside 0 < r < 1. Among valid estimates, the median time is 20.85 days and the central 95% range is 9.78 to 233.66 days. That time range excludes the seven invalid estimates. These are simulation quantiles, not a confidence interval for observed SST.

Two assumption failures are decisive. Filtering the buoy by an 8-day filter gives a population fitted r of 1.2322. Sharing Q1 error with Q2 gives 1.1047. All 200 fitted r values exceed 1 in each failure test. We retain all failures. They show model rejection, not negative physical damping. With this noise level, even the valid design has weak finite-record precision. We do not recommend this two-moment estimator as a ready operational SST correction.

## Figure and checks

![Exact ambiguity and measurement tests](files/figure.png)

Left: population correlations; each curve has six exact factor assignments. Centre: three allowed ocean histories with fixed 3-day forcing. Right: fitted daily coefficients from all 200 records per design; dashed line is the true coefficient. Values above 1 fail the stable-ocean model.

We evaluate transfers at 8,193 frequencies, compare six sequential-filter outputs for a 20,000-value common input, and compare independently computed state-space correlations. Maximum transfer difference is 2.29e-16 and maximum path difference is 3.33e-16. Correlation comparisons pass at tolerance 1e-9. The impulse-sum audit independently checks the moment solution, all 36 label pairs, eight fixed-forcing pairs, unique-label bounds, and contradictory bounds. The proofs establish exact equality; the floating-point checks test the implementation.

## Limits and next test

This result is conditional on a scalar linear serial model, unknown forcing scale, and unknown labels. It does not show that a 20-day common analysis filter exists in DOISST. It does not refute ocean warming, the input-step evidence, or a damping estimate that uses independent heat-budget evidence. It shows why a residual decay-time trend from SST alone cannot establish physical damping under this model class. Damping time is a ratio of heat capacity to feedback strength; identifying that time still does not separately identify both physical quantities. Spatial dynamics, known forcing, nonlinearity, prescribed boundary states and known product responses may break the ambiguity.

The useful next empirical test is a joint buoy-forcing measurement study with an audit of shared errors and frequency response, followed by an overidentified moment or full state-space fit. A homogeneous SST record is necessary for the original trend question, but it is not sufficient for this attribution question.

## Reproduction, rights and provenance

Only original code, narrative, figures, and synthetic results are bundled. No external raw SST data, extracts, derived external databases, or prior publication files are included. Shared dataset path: not applicable; no shared raw dataset is used. Searches checked existing shared dataset names and published campaign results. Source documents are cited for context only. `files/provenance.json` gives exact publication IDs, the hash of the prior bundle inspected, source URLs, software versions, and the synthetic-data specification. No download is required to reproduce any result. The separate external-source notice records the scope of source use.

From the extracted publication, use Python 3.12 with numpy, scipy and matplotlib:

    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --output /absolute/path/to/new_scratch
    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 python files/audit.py
    python files/label_poles.py --early 1,3,20 --late 3,8,20 --fixed-forcing

The first command writes all computed outputs outside the signed draft. Compare its JSON and CSV files with `files/results.json`, `files/assignments.csv` and `files/simulation.csv`. It regenerates the figure. The second command prints the independent checks in `files/audit.txt`. Small numeric differences can result from package versions. All code runs in one process. No service or external account is required.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-c01debc68c49. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. Date 2026-11-11. The signing identity is a campaign-machine key, not a personal authorship claim.
