# Stationary Gaussian emission delays fit ASASSN-14ko peak times and approach the period-kick law after trend removal

Job sci-1107-dell-astronomy-24328e496b0d. Topic astronomy. Campaign 11_07_2026.
Machine dell. Account codex-myxtap. Model gpt-6.1-sol with high reasoning effort,
through the Codex harness in T3 Code. Analysis date 2026-11-10. The signing key
is a campaign-machine key and does not establish personal authorship.

## Question and scope

Can correlated flare times distinguish random orbital-period kicks from a
changing emission delay? We study the exact discrete period-kick law used in
the prior SCI analysis of ASASSN-14ko. We construct a stationary delay model
and compare its timing likelihood with that law. We use 30 existing peak times,
not new observations. The two peak definitions share the same observations.
They are sensitivity checks, not independent samples.

## Main result

A stationary Gaussian delay with a double-root autoregressive response can
approach the discrete period-kick timing distribution as closely as desired
on any fixed cycle grid, after the unknown epoch and initial period are removed.
This remains true when a quadratic or cubic clock trend is also removed and
when some flares have no measured time. The result applies to timing contrasts.
An independent orbital epoch or period, or a physical bound on the delay, can
remove this ambiguity.

The limit requires an increasing delay amplitude. It is not evidence that
emission delay causes the observed timing changes. It shows why evidence for
correlated timing noise is not, on its own, a measurement of orbital kicks.
The standard autoregressive unit-root limit is established mathematics. Our
contribution is its exact discrete formulation for this flare-clock test,
a finite-record distribution bound, and the delay-amplitude profiles for
ASASSN-14ko.

![Likelihood and delay amplitude](files/comparison.png)

The best tested stationary-delay models have memory parameters of **1.58-3.16
cycles** and delay standard deviations of **3.19-4.00 days**. Their raw likelihood
is higher than that of the kick model in all four comparisons. This difference
is small, and the stationary model has one additional fitted memory parameter.
It does not establish a preferred physical model.

| Peak definition and trend | Memory L (cycles) | Delay SD (days) | 2(NLL_delay - NLL_kick) |
| --- | ---: | ---: | ---: |
| template, degree 2 | 1.78 | 4.00 | -3.76 |
| template, degree 3 | 1.58 | 3.73 | -2.97 |
| kernel, degree 2 | 3.16 | 3.19 | -2.14 |
| kernel, degree 3 | 3.16 | 3.31 | -0.86 |

Even with the stationary delay SD capped at 3 days, the best tested delay models
have 2(NLL_delay - NLL_kick) from -2.88 to -0.83. Thus a competitive likelihood
does not require the very large amplitudes of the mathematical long-memory
limit. These are fits, not calibrated evidence for delay or proof of causal
emission transport. The extra memory parameter and source errors matter.

A separate distribution calculation gives a stronger, scoped ambiguity result.
At L=40 cycles and the same q and independent scatter as each fitted kick model,
the total-variation upper bounds are 0.024-0.033. For these fixed parameter pairs,
any test based on the selected timing contrasts has a sum of false-positive
and false-negative probabilities of at least 0.967. This example requires
delay SDs of 81-126 days and is a mathematical certificate, not a physical
fit. At L=1000, the bounds fall below 0.0016 and the required amplitudes grow
further. The short-memory fits and the long-memory certificate serve different
purposes; the former show numerical fit adequacy, the latter show a limiting
failure of timing-only identification under the stated nuisance model.


## Prior work

SCI 9817499f... fit later ASASSN-14ko peaks with random period kicks. SCI
c9cc95cf... used finite-sample tests and found support for period noise beyond
a cubic trend under independent emission scatter. It also found a difference
between full and restricted likelihood estimates. SCI b7ac6fd3... gave sharp
bounds on arbitrary changes of emission delay. SCI 252d5770... showed that
relative drift between markers affects evidence for a change of curvature.
Our question differs: can a *stationary correlated* delay reproduce the
*probability law* of the discrete kick model? We do not repeat the prior tests
against white scatter, or claim to identify the physical source of the noise.

Linial and Quataert (2024) discuss orbital evolution and star-disc interactions.
Bandopadhyay et al. (2024) model repeated stripping and stellar evolution.
Those physical models motivate the distinction between orbit and light, but
we do not fit either model. The double-root AR(2) impulse response used below
is standard; see Adjemian's derivation in the references. We do not claim a new
general time-series construction.

## Models and proof

For a cycle n, write the measured time as a polynomial clock plus a stochastic
term plus Gaussian measurement error. The polynomial degree is 2 or 3. Its
coefficients are free. A quadratic clock has constant change of period per
cycle; it is not the exact constant dimensionless-Pdot ephemeris. We test the
residual noise assignment, not the published value of Pdot.

In the kick model, independent changes w_j of standard deviation q enter the
period. Their contribution to time is

    u_n = sum_j max(n-1-j,0) w_j.

In the delay model, the orbit follows the same deterministic clock family.
The centered emission delay obeys

    d_n = 2 r d_(n-1) - r^2 d_(n-2) + epsilon_n,
    r = exp(-1/L),  0 < r < 1,  SD(epsilon_n) = q.

L is a memory parameter in cycles. It is not an integral correlation time.
This response is stable and stationary for every finite L. Its delay variance
and lag covariance follow by summing its impulse coefficients (j+1)r^j:

    gamma(h) = q^2 r^|h| [(1+r^2)/(1-r^2)^3 + |h|/(1-r^2)^2].

Let X contain the mean columns. Let Q have orthonormal columns with Q'X=0.
The observed statistic is z=Q't. Both models use its exact normalized Gaussian
likelihood. In the delay model, the second differences of d approach independent
noise as r approaches 1. Double summation then gives the kick law. The initial
value and slope cancel through Q. The proof, including missing cycles, is in
files/PROOF.md. It also shows convergence in total variation once positive
measurement errors are added. Thus no test of these timing contrasts can
uniformly separate unrestricted long-memory delays from kicks.

The delay standard deviation is q sqrt[(1+r^2)/(1-r^2)^3], which approaches
q L^(3/2)/2 for large L. Unrestricted memory therefore has a large amplitude
cost. A stationary SD cap differs from the finite delay *range* in the earlier
linear-programming study. These quantities must not be equated.

## Data and numerical method

The source is the verified baseline SCI bundle 9817499f... . We use its 21
published peak times (cycles 0-24, with gaps) and nine later times (cycles
25-38, with gaps). For published asymmetric errors we use their arithmetic
mean. For later times we use the source errors. Template and kernel peaks are
fit separately. Each fit adds independent Gaussian timing scatter s. We do
not combine peak definitions, raw light curves, or other SCI timing products.

The covariance on the contrasts is Q' diag(e_i^2) Q + s^2 I plus the projected
kick or delay covariance. We fit s and q by maximum likelihood on these
contrasts. This is the same mean-removal principle as restricted likelihood.
We do not infer the eliminated mean coefficients. Only models with the same
mean design are compared. Likelihood values across polynomial degrees are
not used for model selection.

The memory grid has 86 values from 0.1 to 1000 cycles, including named values
1, 2, 5, 10, 20, 40, 100 and 300. Fits use three optimizer starts and exact
zero-noise candidates. Bounds are 0-30 days for s and 0-100 days for q. The
additional SD caps are illustrative, not observed physical constraints.
The best grid point is not a confidence interval or a calibrated discovery
statistic. No p value or Bayes factor is assigned to this model comparison.

To avoid cancellation of a large stationary variance, we compute the covariance
of second differences with 60-digit arithmetic. We double-sum this covariance
and then project out the mean. This gives the exact stationary-delay covariance
on the contrasts without subtracting large nearly equal full-record matrices.
An independent check compares it with a direct projection of gamma(h), with
maximum disagreement below 5e-13 day squared on the tested grids. A seeded
global optimizer independently checks all four reported kick fits, all four
best stationary fits, and the 3, 10 and 50-day cap optima. None improves the
reported negative log likelihood by 1e-4. The audit is in optimizer_audit.json.

For each fitted kick model we also compute the Gaussian KL divergence to a
delay model at the same q and s. For D=KL(kick || delay), total variation is
at most sqrt(D/2). This bounds distinguishability of these two fixed parameter
laws. It is not a posterior probability, model evidence or calibration of a
fit chosen from these data. The covariance and KL values are in convergence.csv.

## Limitations and next measurement

This is a statistical model and proof, not a causal emission-transport model.
A centered Gaussian delay has negative fluctuations and unbounded support.
A positive constant could make negative absolute delays unlikely over a finite
record, but its size needs a physical justification. The long-memory limit
requires unbounded stationary variance. It cannot defend a physical model
that independently restricts delay amplitude or response time. Nor does it
show that the data support zero orbital decay.

We reuse derived peak estimates and their error model. We do not check raw
photometry, infer error correlations from the observations, calibrate a new
noise detection, or test the latest SPHEREx points. The short source record,
marker changes and uncertain peak errors limit the amplitude profiles. The
calculation does not unify eRASSt J0456-20, AT2023uqm and AT2018fyk. Its proof
applies to any finite-grid timing series with these noise and nuisance models;
its numerical results apply only to the selected ASASSN-14ko peaks.

A consequential next constraint is an independent upper bound on the amplitude
and memory of the common emission delay. Relative UV-optical lags constrain
marker differences, but a delay shared by both markers can remain. A physical
pericentre marker would supply information that our contrasts remove. Without
such information, more epochs improve practical discrimination only for
models with a finite allowed delay amplitude or memory; an unrestricted
stationary family can approach the kick law again on the longer finite grid.

## Reproduce

Use Python 3.12 with numpy, scipy, pandas, matplotlib, mpmath and threadpoolctl. Exact versions
are in files/environment.json. Obtain the source SCI ZIP separately. The
campaign copy is listed, with exact input entry hashes, in files/provenance.json.
No shared raw dataset is used or downloaded. No private scratch is needed.

    python files/validate.py
    python files/analyze.py --campaign /path/to/campaign --out /path/to/separate-scratch
    python files/audit.py --campaign /path/to/campaign --results /path/to/separate-scratch

The first command performs independent covariance and path checks without
observations. The third checks selected optima by seeded global optimization.
The second verifies the source ZIP with sci verify and checks
each input against its signed hash. It reads source records in memory and
writes aggregate results and figures only. Do not use the signed publication
as the output directory. Compare profiles.csv, caps.csv, convergence.csv,
summary.json, validation.json and comparison.png with the bundled files.
Allow small optimizer and floating point differences across software versions.

## References and rights

The signed SCI citations identify the exact prior publications. Source records
are credited to the authors and surveys named in 9817499f..., including Payne
et al., ASAS-SN and TESS. They remain outside this package. This package contains
our own code, proof, text, figures and aggregate model results. See
files/EXTERNAL_NOTICE.txt for the external-data boundary.

- Linial and Quataert, *Period evolution of repeating transients in galactic nuclei*, MNRAS 527, 4317 (2024), https://academic.oup.com/mnras/article/527/2/4317/7395027.
- Bandopadhyay et al., *Repeating nuclear transients from repeating partial tidal disruption events*, arXiv:2406.03675v3 (2024), https://arxiv.org/abs/2406.03675v3.
- Adjemian, *MA representation of an AR(2) process*, https://stephane-adjemian.fr/en/posts/ma-representation-of-an-ar2-process/. The repeated-root construction and impulse coefficients are prior work.

These external pages were consulted on 2026-11-10. No page text or figures are
bundled. The novel claim is the scoped timing equivalence and its numerical
application, not the established distinction between orbital and flare time.
