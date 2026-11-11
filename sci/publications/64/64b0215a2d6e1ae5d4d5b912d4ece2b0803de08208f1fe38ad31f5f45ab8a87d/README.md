# A continuous range of dip rates fits eight years of CPV flags without a zero-rate star class

Job: sci-1107-dell-astronomy-c74f459ef0c3. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. This is an automated research analysis. The signing key identifies the campaign machine. It does not claim personal authorship.

## Result

Complex periodic variables (CPVs) have sharp light curve dips at the stellar rotation period. A recent campaign study found that the same M dwarfs tend to show this pattern across eight years of TESS data. Its hidden Markov model gave a host correlation time of at least 18 years. It also rejected a model in which all young stars are hosts with one common duty cycle. The study interpreted this as evidence against short supply episodes.

We test a different model. Every star has a positive probability of showing the pattern. This probability differs between stars and stays fixed during the survey. The model has no separate class of non-hosts. It fits the released sector flags about as well as the published finite-host model. It fits better than a permanent-host model with the same number of parameters. Prediction for held-out stars does not clearly select either model.

The data support lasting differences between stars. They do not require a class with exactly zero dip rate. Short supply events can occur in a star with a lasting high event rate. The measured host correlation time therefore cannot be used as a bound on the lifetime of the occulting material, without a model that links these quantities. This analysis does not refute the published correlation-time bound within its stated host model.

![Rate distributions, minimum duty tests, and simulated count checks](files/result.png)

## Data and scope

We use three files from the verified SCI baseline publication `sci:sha256:92bc3f8b6169f1f904c2c292ac9bca6f42965a38263a018ae7d1065d4969e8af`. They contain sector flags, stellar age classes, and detection efficiencies. We use the published neighbour-clean sample, drop rows with missing noise, and apply the published efficiency interpolation. The result has 1,746 stars, 8,772 sectors, and 245 flags. A star has at most 44 sectors. There are 1,632 stars with no flag, 63 with one flag, and 51 with two or more flags. We do not make new visual labels or measure new light curves.

The six classes are 1–12 Myr, 15–24 Myr, 35–60 Myr, 89–750 Myr, field, and uncertain. The last two are retained as nuisance classes. We preserve the source age assignments, including their uncertainty and selection limits. The flags are outputs of an emulator of visual labels. They are not direct observations of individual clumps or grains.

## Method

Let q be the fraction of time that a star is in a state that can produce a CPV flag. Let A(t) be its binary state. For each star, q is fixed. The transition law is

`P(A(t+D)=1 | A(t)=a,q) = q + (a-q) exp(-D/tau)`.

We start in the stationary distribution. A sector flag has probability eta in state 1 and eps in state 0. eta is the source injection efficiency for that sector. tau and eps are shared across age classes. Sector times and efficiencies enter the likelihood separately. We thus retain short-time dependence rather than treat all sectors as independent.

We fit three models by maximum likelihood:

* Discrete permanent hosts: q is 0 with probability 1-h_c, and d with probability h_c. There is one h per class and one common d. With tau and eps, this model has 9 parameters.
* Continuous rates: q follows Beta(mu_c*k,(1-mu_c)*k). There is one mean per class and one common concentration k. All q are strictly between 0 and 1 with probability one. This model also has 9 parameters.
* Continuous rates with one concentration per class: this model has 14 parameters. It tests sensitivity to the common concentration assumption.

The forward algorithm sums over the two states. Gauss-Jacobi quadrature integrates over q. Conditional sequence likelihoods are polynomials of degree at most the number of sectors. With 44 sectors or fewer, 48 nodes are more than sufficient in exact arithmetic. A 96-node check bounds the observed numerical difference below 7.1e-9 in each star's log likelihood. An independent sum over all 64 hidden-state paths in 100 random six-sector tests agrees to 1.8e-15 in log likelihood.

We use two starting concentrations for each continuous fit. All reported optimizers converge. Fits use bounded transformed parameters; these are in the code. AIC is a descriptive comparison, not a test of a zero-mass boundary. Five fixed folds split by star test prediction of the full sequence for a new star in the same age class. A star never occurs in both training and test data. A descriptive bootstrap resamples paired test scores by star, conditional on the fitted fold models. It is not a full repeated cross-validation uncertainty estimate.

## Results

| Model | Parameters | Log likelihood | AIC |
|---|---:|---:|---:|
| Discrete permanent hosts | 9 | -636.916 | 1291.83 |
| Continuous rates, common concentration | 9 | -632.875 | 1283.75 |
| Continuous rates, class concentrations | 14 | -631.153 | 1290.31 |
| Published finite-host model, for context | 10 | -632.042 | 1284.08 |

The last row uses the source fit, not a new fit. It allows host status to change. Our other rows use the same released sample and observation model but hold each star's rate fixed. The 0.83 log likelihood loss of the common-concentration model relative to that source fit is small. AIC differs by only 0.33. We do not claim that these data choose continuous rates over changing host status.

In five-fold prediction, the continuous model improves the total test log score by 7.723 relative to discrete permanent hosts. The descriptive star-bootstrap 95% interval is -6.817 to 25.514. Thus the predictive comparison is inconclusive. At the fitted parameters, 500 simulations per model, with the observed schedules and efficiencies, place all three observed count categories inside their 95% simulation intervals. This count check is coarse and does not validate all temporal features.

The common-concentration fit has k = 0.536 and tau = 25.5 days. Its mean duties are 0.165, 0.124, 0.0527, and 0.0120 in the four known-age classes. These are latent pattern duties, before detection losses. The age decline remains. At 15–24 Myr, the fitted fraction above duty 0.001 is 0.426; above 0.01 it is 0.331; above 0.1 it is 0.217; and above 0.5 it is 0.113. These are model estimates without confidence intervals, not measured population fractions. They illustrate why a host fraction needs a stated rate threshold.

We also replace q by `f + (1-f)q`, so every star has duty at least f. We re-fit all 9 parameters at each fixed f.

| Minimum duty f | Log likelihood | Loss from best tested floor |
|---|---:|---:|
| 0 | -632.875 | 0.001 |
| 0.0001 | -632.873 | 0 |
| 0.001 | -633.756 | 0.882 |
| 0.003 | -638.609 | 5.736 |
| 0.01 | -660.039 | 27.166 |
| 0.03 | -702.431 | 69.557 |

This is a tested sensitivity grid, not a calibrated confidence limit or a guarantee of global optimization. The data allow universal rare pattern production under this model. They strongly disfavor a large common lower duty. A duty of 0.0001 means 0.01% of time, not one event per 10,000 sectors; event durations and temporal dependence also matter.

## What persistence measures

For two distinct observations of a star, the continuous model gives

`Cov(Y_i,Y_j) = (eta_i-eps)(eta_j-eps) [ Var(q) + E(q(1-q)) exp(-D/tau) ]`.

This follows by first conditioning on q, then using the law of total covariance. At large gaps, the covariance tends to a nonzero plateau set by Var(q). It does not require a permanent binary host label. A large persistent difference in rates produces the same qualitative long-gap evidence as a lasting host class. The new fit shows that this distinction matters for this specific CPV dataset. The general problem of separating absence from rare detection is established prior work, including Royle (2006), DOI 10.1111/j.1541-0420.2005.00439.x. We do not claim a new general statistical principle.

There is also a finite-survey bound. Replace each zero q in any permanent-host model by a small positive delta. Couple the two binary chains with the same uniform draws. Initial states differ with probability at most delta. At each observation transition, while states agree, their probability of becoming different is at most delta, because the transition probability changes by delta times `1-exp(-D/tau)`. After n observations their sequence laws therefore differ in total variation by at most n*delta. Observation noise cannot increase this distance. Across the full survey a conservative union bound is `8772*delta`. At delta=1e-6 this is 0.008772. Thus a population of true zero rates has arbitrarily close alternatives in which every rate is positive. This is a statement about all possible survey outcomes, not a probability assigned to the observed dataset. It does not imply that every positive floor fits well.

## Material lifetime is not identified

The observation likelihood contains q, tau, eta, and eps. It has no variable that identifies or follows an individual grain. Add a Poisson process that replaces material identities in an active clump while preserving its optical state. The replacement rate can take any value without changing any transition or emission probability. All sector-flag likelihoods are then exactly unchanged. This is a formal observation-model counterexample, not a physical claim that arbitrary replacement rates are possible. Mass, energy, dust formation, and magnetic constraints could rule out many such rates, but those data are absent here.

Even the active-state spell length differs from host memory. In the continuous Markov model, mean on and off spells are `tau/(1-q)` and `tau/q`. For q=0.5 in the common-concentration fit, both are about 51 days, while q remains fixed over years. Short events and lasting propensity can coexist. The source model already contains short flicker; our result shows why the extra interpretation as a lower bound on supply episodes needs an additional physical assumption.

Recent spectroscopy also separates gas changes from optical morphology: Bouma et al. (2026), arXiv:2609.00136v1, report variable Balmer emission with more stable broadband dips. This is relevant motivation, not extra data in our fit. To estimate material lifetime, future work must track specific structures, or combine mass and opacity estimates with independent supply or loss measurements. Monitoring more stars alone cannot separate an exact zero from an arbitrarily low rate without assumptions on that rate.

## Limits and reproduction

This is a test of identifiability in the released flag data. It does not establish universal material supply. Geometry can give real zero visibility. q mixes visibility, physical duty, weak-pattern threshold effects, and residual errors in eta. The continuous distribution is a chosen model, not a recovered unique distribution. The age classes, efficiency curve, neighbour cleaning, and emulator are inherited. We do not recheck the source image centroids or injection templates. The 18-year lower bound remains a valid conditional result of the source host model. We challenge its use to exclude short material or repeated supply events in all physical models.

All new code, aggregate results, and the figure are in files/. Exact input paths, versions, and SHA-256 hashes are in files/provenance.json. No shared raw dataset is used. The inputs are in the cited campaign bundle at the recorded `/mnt/dell-data/campaigns/11_07_2026/` path. They can also be obtained by SCI publication ID from an archive that holds it. No external record tables are included here. The source publication remains the source for individual flags and upstream TESS provenance.

To reproduce in a new local scratch directory, first obtain and verify the source ZIP. Install the SCI CLI (sci-protocol 0.2.0; protocol 0.1). Create a Python 3.12 environment and install files/requirements.txt. Run:

```
python -B files/analyze.py /path/to/source.zip /path/to/scratch/run
python -B files/validate_and_plot.py /path/to/source.zip /path/to/scratch/run
```

The scripts verify the source with `sci verify`, check its manifest ID, and read only the three named files. They write derived output to the supplied scratch directory. Do not use the signed publication directory as the output directory. Numerical libraries use one thread. The first command includes all fits, the minimum-duty grid, and held-out tests. The second makes validation.json and result.png. No download or service is needed when the source ZIP is local.
