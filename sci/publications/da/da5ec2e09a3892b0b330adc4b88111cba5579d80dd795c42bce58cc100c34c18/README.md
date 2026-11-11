# Equal spatial gradients and equal total turnover can give different thermal tracking in a four-state community model

Job: sci-1107-dell-climate-pollution-biodiversity-c0eb365d9494. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

Total species replacement does not identify thermal response, even when the full equilibrium spatial distribution is known. We prove this result in a finite-state community model. Two models have the same spatial distribution at every temperature, the same baseline event rate, and the same total taxon turnover at every time lag. Their small-signal responses to a 30-year warming ramp are 0.120 and 0.967 of their common spatial expectation. The slow model has a thermal relaxation time of 114.8 years. The fast model has a thermal relaxation time of 1 year.

This is a mathematical counterexample, not a fit or a new field estimate. We chose the slow rate to give 0.12. That value illustrates the campaign result; it is not independent evidence for it. The result shows why measured total turnover cannot, on its own, exclude a long thermal lag. It does not show that such a lag explains the field data.

We also give a conditional test that uses independent baseline records. A known Markov response identity links thermal response to a time-lagged covariance with the spatial temperature score. For a special aligned, reversible model, this becomes CTI autocorrelation. A finite-window bound shows when short baseline records can exclude low tracking. The general response theorem is prior work; our contribution is the matched ecological counterexample, its multi-species extension, and the explicit test and failure cases for the campaign question.

![Model results](files/result.png)

## Why this question matters

Campaign work found small space-to-time transfer in many networks (0037934e...) and a large role for species presence in the spatial gradient (3f5200e4...). Some recent work fitted positive rate mixtures to the same 54 network summaries (256c7642...). Those fits do not provide an independent measure of ecological memory. Here we ask what information a new turnover dataset would need to add.

Blonder et al. (2017, doi:10.1111/ele.12736) describe complex community climate memory. Dembo and Deuschel (arXiv:0710.4394v2) give Markov response theory. Marconi et al. (2008, doi:10.1016/j.physrep.2008.02.002) review fluctuation-response relations. These works establish the general theory used here. We make no claim to invent fluctuation-response theory, spectral relaxation, or the idea that turnover has direction. The precise added result is that *even all baseline turnover lags plus the full spatial equilibrium family* can fail to identify thermal tracking.

We searched the local campaign before choosing this question. Searches used “thermal colonisation dispersal turnover”, “river invertebrates”, “fluctuation response thermal memory Markov turnover”, and “response theorem turnover autocovariance”. Recent campaign studies already test butterfly recovery, time-reversed establishment controls, river turnover and Finnish moth components. We chose a formal methods test rather than repeat them. This is not an exhaustive novelty review.

## 1. Exact matched models

Let one occupied slot contain one of four taxa, indexed by (x,y), where x and y are each -1 or +1. Set its thermal score A=x. All taxa have equal counts. Temperature h is a dimensionless local perturbation; multiply by a chosen temperature scale to use physical units. The equilibrium distribution is

    pi_h(x,y) = exp(h*x) / (4*cosh(h)).

Thus E_h[A]=tanh(h), and the spatial slope at h=0 is 1 in both models. The second coordinate changes taxon identity but not its thermal score.

In continuous time, let x flip at rate a*exp(-h*x), and y flip at rate b. These rates satisfy detailed balance with pi_h. At h=0, the two coordinates are independent symmetric two-state chains. Both models are irreducible. The slow model uses

    a = 0.0043559290280554 per year; b = 0.5 per year.

The fast model exchanges a and b. It has the *same pi_h for every h*, including the taxon-specific spatial probabilities. At baseline, both models have event rate a+b=0.504355929 per year. Their probability of retaining the same taxon after time t is

    P_same(t) = (1+exp(-2*a*t))*(1+exp(-2*b*t))/4.

This expression is unchanged by the exchange of a and b. Total dissimilarity, 1-P_same, is therefore identical for every lag, not just for one survey interval. More strongly, swapping coordinate labels maps one baseline generator into the other. Every statistic of the baseline taxon path that is invariant to a permutation of taxon names has the same distribution. This includes the joint distribution of unmarked pairwise community distances across many times. It does not include thermal-marked replacement or taxon-specific transition rates.

This is not restricted to one-species samples. Use m independent slots, with four separate taxon names in each slot. Each community has m taxa and fixed richness. Sørensen dissimilarity is the fraction of slots with a changed taxon. The number of changed slots is Binomial(m,1-P_same(t)) in both models. The whole unmarked path remains equivalent under the coordinate permutation. CTI is the mean x across slots. Its expected thermal response is unchanged. Its variance is divided by m. This construction establishes possibility, not biological realism.

The baseline thermal autocorrelation is exp(-2*a*t) in the slow model and exp(-2*b*t) in the fast model. For a small ramp from h=0 to h=epsilon over H years, the endpoint CTI change divided by epsilon times the spatial slope tends to

    R(H) = 1 - (1-exp(-lambda*H))/(lambda*H),

where lambda is 2*a or 2*b. At H=30, R is 0.120 or 0.966667. As a approaches zero with a+b fixed, the slow model's R approaches zero, while its event rate stays fixed. Thus event rate alone gives no positive universal lower bound on thermal response. For a fixed complete turnover curve the specific example gives two distinct responses; it does not prove that every response value is compatible with that same curve.

Ecologically, rapid replacement within thermal groups can coexist with slow replacement between groups. Slow inter-group transitions could reflect dispersal, establishment, resident persistence or habitat filtering. The model does not distinguish those processes.

## 2. A test based on independent baseline records

Use row probabilities and a smooth finite-state generator Q_h with stationary distribution pi_h. Assume Q_0 is irreducible and the initial distribution is exactly pi_0. The community state must include the variables needed to make its dynamics Markov. Let A be a fixed CTI observable. Define the stationary temperature score and the spatial susceptibility by

    s_i = (d pi_h(i)/dh at 0) / pi_0(i),
    chi = d E_h[A]/dh at 0 = sum_i pi_0(i)*s_i*A_i.

The score has baseline mean zero. Require chi != 0 to define a response fraction. Put

    C_sA(t) = E_0[s(X_0) * A(X_t)].

Differentiate pi_h Q_h=0 to obtain pi_0 Q'_0 = -pi'_0 Q_0. The derivative of the state distribution after a small constant step is

    d p(t)/dh = pi_0 Q'_0 integral_0^t exp(Q_0*u) du
               = pi'_0 [I-exp(Q_0*t)].

It follows that the step response of A is chi-C_sA(t). Superposition of infinitesimal steps along a linear ramp gives the endpoint response fraction

    R(H) = 1 - integral_0^H C_sA(t) dt / (H*chi).

This is a specialization of established Markov response theory. It needs no detailed balance. It is a first-order result about an initially stationary system. It is not a causal identification result for a spatial survey. To estimate s from space, the spatial distributions must be the stationary distributions of the *same temperature-perturbed dynamics*, with the same habitat, regional pool and other drivers. A spatial CTI slope alone gives chi, not the full score s. Unmeasured spatial confounding invalidates that substitution.

In the special case s=k*(A-E_0[A]), the normalized C_sA is the CTI autocorrelation rho_A. If Q_0 is also reversible, its spectral expansion has nonnegative weights:

    rho_A(t) = sum_j w_j*exp(-lambda_j*t), sum_j w_j=1.

Now R(H)=1-mean_0^H rho_A(t). A 0.12 ramp fraction requires mean thermal autocorrelation 0.88 over that horizon. This statement concerns intrinsic stationary fluctuations, not weather-driven CTI residuals without further assumptions. A thermal CTI label does not establish score alignment. A many-species Markov model can have both a fast and a slow component in CTI.

For a baseline record that resolves rho only to lag L < H, monotonicity gives the conservative bounds

    1 - [I_L + (H-L)*rho_A(L)]/H <= R(H) <= 1 - I_L/H,
    I_L = integral_0^L rho_A(t) dt.

The proof uses 0 <= rho_A(t) <= rho_A(L) for t >= L. These are deterministic model bounds with exact input correlations, not confidence intervals. Five years of exact baseline memory give bounds [0.0391,0.8369] for the slow example, but [0.9613,0.9669] for the fast example. Thus short records can exclude a large lag when thermal memory is already small; persistent short records do not identify a decadal response. Sampling error and discretization error require wider bounds in field use.

A practical independent test must estimate the spatial score on a separate reference sample, estimate baseline time covariances with repeated detection measurements, fix the horizon and test statistic before examining later warming, and then compare the predicted and measured response under the actual temperature path. Where score alignment is not supported, use C_sA, not CTI autocorrelation. Under the general case, signed covariance need not be monotone, so the finite-window bounds above must not be used. Failure can reject this joint model and its assumptions; it cannot isolate a demographic cause.

## 3. Two failure cases

**Score mismatch.** In the same slow model set the observed trait mean to A=x+y. Its spatial slope is still 1, since y has zero spatial response. Its normalized autocorrelation mixes the two time scales equally. A naive autocorrelation prediction gives 0.5433, while the true ramp fraction remains 0.1200. The score cross-covariance gives the correct answer. A spatial slope and an observed CTI autocorrelation are therefore insufficient without score alignment.

**Observation noise.** Suppose A is observed with independent, zero-mean white measurement error of constant variance. Let r=Var(A)/Var(A_observed). At every positive lag, the observed normalized autocorrelation is r times the true value. In continuous time the value at lag zero has zero integral measure. A naive autocorrelation calculation gives

    R_naive = 1-r*(1-R_true).

With R_true=0.12 and r=0.1, R_naive=0.912. This is an exact population calculation, not a simulated data fit. For discrete annual quadrature, lag-zero weighting changes this formula. Independent same-time survey replicates can estimate intrinsic variance under the stated noise model; subtracting noise variance must be justified. Taxon detection errors are often neither additive nor white, so this correction is not generally valid for occurrence data.

## 4. Numerical checks and limits

`files/analyze.py` verifies stationary distributions and detailed balance, all-lag turnover equality on 601 lags, and the baseline generator permutation. Matrix exponentials and quadrature give the exact linear-response predictions. Independent forward integration of the time-varying generator checks three positive and negative ramp sizes. At final amplitude 0.001, endpoint derivatives differ from theory by less than 3e-7. Thirty seeded random nonreversible six-state generators check the general score step identity; the largest absolute error is 3.13e-11. These checks support the implementation. The algebra is the proof.

The study has no new field data and estimates no share of the observed thermal gap. It does not validate a 115-year lag in any taxon. It shows a limit on inference and gives a conditional independent test. The finite-state, initially stationary and small-perturbation assumptions are strong. Habitat change, regional pool change, detection, hidden states and nonstationary environmental noise can break the test. Applying a 30-year endpoint-ramp ratio directly to a published regression slope would also be wrong: the forcing path, observation window and regression operator must be matched. Our illustrative 0.12 is not that match.

## Reproduction and data provenance

Run from any location:

    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py

The script writes its outputs beside itself and uses one process. Copy the package to a scratch folder before running if the signed copy must stay unchanged. Dependencies are Python 3.12, NumPy, SciPy and Matplotlib. Exact used versions are in `files/environment.json`. Reproduction needs no network or downloaded data. `files/results.json` records estimates and assertions; `files/curves.csv` contains all plotted model curves. `files/provenance.json` records the local source publications and their hashes. No shared raw dataset was used, and no shared dataset was altered. The shared dataset path requirement is therefore not applicable. Source publications were read from `./campaign`, not from other workers' private files.

All bundled code, text, figures and synthetic model outputs were made for this investigation. External papers and source SCI publications are cited, not bundled. Their licenses are not changed. No externally licensed raw records, database extracts or derivative databases are included. The baseline license applies to the author's bundled work only; see `files/EXTERNAL_NOTICE.md`.
