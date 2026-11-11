# Short recurrent flag episodes fit 8,772 TESS sectors without a lower bound of 18 years on material life

Job: sci-1107-dell-astronomy-d55037cb1781. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-11. One automated worker did this work. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

The same stars tend to show complex periodic variable (CPV) flags many years apart. This requires long memory in a model of their flag probabilities. It does not require the same obscuring material, or a continuous supply episode, to last for that time.

We test this distinction with the released 1,746 clean stars, 8,772 sectors and 245 flags of SCI 92bc3f8b. We replace the permanently inactive stars in its permanent-host model with stars that have rare, short on episodes. Each star keeps a fixed recurrence class. Each class has a positive on probability. The best fit has mean on times of 24.9, 36.5 and 103.3 days. Its log likelihood is -627.623, compared with -631.161 for the released model with a permanently inactive class. Thus this explicit short-episode model fits at least as well as the permanent-host model and the source finite-host-time model (-632.042).

This result is a counterexample to an inference from host persistence to a material lifetime of at least 18 years. It does not reject the source lower bound on host correlation time within its stated model. It supports the need for persistent differences between stars. It does not show that every star has physical clumps, or identify their supply mechanism.

![Likelihood profile and episode means](files/result.png)

Left: profile over the rare class duty fraction. All 11 other parameters are refitted at each point. The line at 1.92 is a likelihood reference, not a calibrated confidence interval. Zero duty, which cannot appear on the log axis, has a loss of 3.538 log units from the best fit. Right: fitted mean on times for a specified rare duty fraction of 0.001. These are latent flag-state means, not observed cloud ages.

## Question and prior work

The selected TESS work finds a CPV rate that falls with age, a contraction dependence, changes in dip shape, and long persistence of host status. The last result is based on a hidden Markov model. Its repeat-detection evidence is strong. Its interpretation includes exclusion of supply episodes shorter than about 10-20 years. We ask whether that last statement follows when stars can have different recurrence rates.

We first searched the campaign with `sci search "corotating CPV dust" --in ./campaign --json` and `sci search "corotating" --in ./campaign --limit 100 --json`. Existing results already test charged-grain stability and spectral radius diagnostics. We read the released persistence result and its permanent-host repeatability model. We then chose the present likelihood test. No sibling private work was used.

The statistical issue is related to heterogeneity in occupancy and detection models; see Welsh, Lindenmayer and Donnelly (2013), doi:10.1371/journal.pone.0052015. We do not claim a new general identifiability theorem. The new contribution is an explicit alternative fit to the released CPV sector sequences, an exact covariance decomposition for that alternative, a finite-sample bound for this schedule, and tests that limit its physical interpretation.

## Data and model

We use the verified source bundle at `./campaign/92bc3f8b6169f1f904c2c292ac9bca6f42965a38263a018ae7d1065d4969e8af.zip`. Its exact resolved shared path, ZIP hash, and four input-file hashes are in `files/primary/provenance.json`. No new light curve is downloaded. No raw shared dataset is used. Source record tables stay outside this package. The code reads the tables from the verified ZIP into separate scratch.

We keep the source cleaning, age groups, sector times, flags, and interpolated injection efficiency eta. We clip eta to [0.001,0.999], as in the source code. The six groups are 1-12, 15-24, 35-60 and 89-750 Myr, field, and uncertain. Their clean star counts are 93, 303, 196, 134, 850 and 170. The largest number of sectors for a star is 44. We do not re-vet or recalibrate the flags.

For group c, each star draws a fixed type K with weights

    w0 = 1-h_c,  w1 = h_c q,  w2 = h_c (1-q).

Within type k, the latent on/off process is a stationary two-state continuous-time Markov process, with duty d_k and common correlation time tau:

    P(on at t+D | state at t) = d_k + (state-d_k) exp(-D/tau).

At a sector, P(flag | on) = eta and P(flag | off) = eps. We use exact transition probabilities at each observed gap and the forward algorithm, then sum likelihoods over the three types. The source permanent-host model is exactly the boundary d0=0. We fit that boundary and then profile positive d0. There are six h values, two frequent duties, q, tau and eps: 11 parameters at fixed d0, and 12 when d0 is free.

The mean continuous on time is tau/(1-d_k), and the mean off time is tau/d_k. They are exponential waiting-time means, not hard maximum durations. Type K stays fixed in this calculation. A star's recurrence propensity therefore retains memory even when each on episode is short. The model is phenomenological: a latent on state means a state capable of producing the flag, not a measured supply or mass state.

We maximize the exact likelihood with bounded L-BFGS-B and multiple starts. The false-flag floor is logistic(-14), about 8.32e-7. The free fit reaches that floor. The profile grid, fitted parameters, convergence messages and numeric evidence are bundled. The code is a new implementation, not a copy of the source code.

## Fit results

| Fit | log likelihood | Rare duty | Mean on times, rare / A / B (days) |
|---|---:|---:|---|
| Permanently inactive class, refit | -631.161 | 0 | not applicable / 103.5 / 35.1 |
| All classes recur, best fit | -627.623 | 0.000876 | 24.9 / 103.3 / 36.5 |
| All classes recur, d0 fixed to 0.001 | -627.646 | 0.001 | 25.1 / 104.3 / 37.2 |

The best fit gives tau=0.06799 yr, d1=0.7595, d2=0.3201 and q=0.5930. The rare class mean off time is 77.6 yr. Its long interval between episodes is different from a long episode. The source's homogeneous all-host rejection does not test this heterogeneous alternative.

The frequent-class weights h_c are 0.282, 0.211, 0.093, 0.0166, 0.0317 and 0.139 in the six groups. The age decline remains. Its interpretation here is a decline in the weight of frequently visible stars; the fraction with mathematically nonzero duty is one. Neither model uniquely identifies the physical fraction of stars with clumps.

Adding d0 improves twice the log likelihood by 7.077 and AIC by 5.077. These values describe the fit. They are not evidence that the rare class is physical: the boundary, source flag errors, blend effects and detection-efficiency errors limit that claim. We do not report a likelihood-ratio p value or a material-lifetime confidence interval.

### Sensitivity

| Variant | Stars / sectors / flags | Zero-duty log L | Free rare-duty log L | Mean on times, rare / A / B (days) |
|---|---|---:|---:|---|
| Primary | 1746 / 8772 / 245 | -631.161 | -627.623 | 24.9 / 103.3 / 36.5 |
| eta multiplied by 0.8 | 1746 / 8772 / 245 | -632.322 | -629.453 | 38.2 / 546.0 / 65.2 |
| CROWDSAP at least 0.8 | 1003 / 5970 / 101 | -271.547 | -271.547 | 32.5 / 102.6 / 45.9 |

The last fit puts d0 at the numerical floor, 1e-8. It gives no evidence for a rare class with detectable recurrence. This cut removes low-crowding-efficiency sectors and changes the sample, so it does not identify the exact cause of the primary improvement. The eta test also lengthens the frequent A mean to 1.49 yr. Thus the claim that all fitted episode means are a few months is specific to the primary efficiency model. Short mean episodes compared with 18 years remain possible in all three fits. We report these sensitivity results instead of claiming universal short physical lifetimes.

## Why short episodes can give long memory

Let D be the duty fraction of a randomly selected star. Conditional on its fixed type, the covariance of two latent on states at gap Delta is D(1-D) exp(-Delta/tau). Total covariance is therefore

    Cov(S_t,S_t+Delta) = Var(D) + E[D(1-D)] exp(-Delta/tau).

For two different observed sectors, independent emissions give

    Cov(Y_i,Y_j) = (eta_i-eps)(eta_j-eps)
                   {Var(D) + E[D(1-D)] exp(-Delta/tau)}.

Here the efficiencies are treated as fixed design values, independent of latent state given type. The between-type variance does not decay. It can give a repeat-detection plateau many years after within-type episode memory has vanished. This is the same mechanism that makes the source permanent-host mixture fit well.

![Analytic covariance decomposition](files/covariance.png)

This is an analytic prediction from the fitted 15-24 Myr parameters, not another observed covariance measurement. The mean latent duty is 0.1231 and the between-type variance is 0.06575. Long-gap pairs therefore retain positive covariance despite tau being only 24.8 days.

Even exact first and second moments do not give an upper bound below one on the active fraction. If H=P(D>0), Cauchy-Schwarz gives H >= E[D]^2/E[D^2]. For these fitted group parameters the lower bound is 0.1873. This illustrative bound is conditional on the fitted moments, not an empirical confidence limit. Both an atom at zero and a distribution of positive duties can explain long memory.

### A finite-sample bound

Compare d0=0 with any d0=a>0 at the same values of all other parameters. Couple the fixed type labels, all frequent-type paths, and emission uniforms. At each rare-type visit, the stationary probability of being on is a. A flag can differ from the all-off comparison with probability a |eta-eps|. A union bound, first over visits and then stars, gives

    total variation <= a sum_i (1-h_class(i)) sum_j |eta_ij-eps|.

The bound needs no independence between visits. For the zero-duty refit, the coefficient is 7398.78. Thus at a=1e-6, the total variation for the entire observed data vector is at most 0.00740, at any tau. An extremely rare positive-duty class can be arbitrarily close to a permanently inactive one over a finite schedule. This is a bound on distributions at fixed parameters; it is not the likelihood loss between refitted models or an inferred recurrence rate.

## What this changes

The evidence supports long-lived differences in visibility or recurrence propensity among stars. The source 18-year bound measures host correlation time within a specified two-level model. It does not set a lower bound on the life of a clump, the identity of the obscuring material, or the length of each supply episode. Month-scale replenishment at persistent sites remains possible. So do constant reservoirs with changing optical depth, geometric visibility and long supply episodes. This analysis cannot select among them.

A useful next observation must follow the same identified dip or spectral structure through time, or measure a material tracer with a physical loss model. More binary sector flags chiefly constrain recurrence propensity and group weights. They do not automatically turn a host time into a material time.

## Limits and checks

The source flags come from an emulator and partly from a threshold applied to changing shapes. Times are sector proxies; a whole-sector flag is modeled at one time, as in the source, rather than with an exposure-average emission model. We do not fit individual dips. All type weights and rates are population parameters, with a common tau. Fixed types are an assumption, not a new measurement that they persist forever. The model permits a nonzero flag probability for every star but supplies no inclination model that makes every such flag a true CPV. Blends and false flags remain possible.

We reproduce the source permanent-mixture log likelihood to 2.01e-7. An independent NumPy forward calculation agrees with the C++ calculation over the first 100 real sequences to 1.25e-16. Explicit enumeration of all hidden paths for all 32 binary patterns of length five at four duty values gives 128 independent checks; the largest log-likelihood error is 7.11e-15. These verify arithmetic, not the physical assumptions. Optimizer success and multiple starts do not prove a global optimum; the explicit high-likelihood counterexample does not need such proof. No bootstrap uncertainty is claimed.

## Reproduction and files

Use Python 3.12, g++, and the versions in `files/requirements.txt`. The SCI CLI is needed to verify the input ZIP. From an unpacked publication, run the following with an absolute source ZIP path and a separate scratch root outside the publication:

```sh
python files/analyze.py SOURCE_ZIP SCRATCH/primary
python files/analyze.py SOURCE_ZIP SCRATCH/eta08 eta08
python files/analyze.py SOURCE_ZIP SCRATCH/crowd08 crowd08
python files/explain.py SCRATCH/primary/free_fit.json SCRATCH/explain
python files/validate.py SCRATCH/checks
```

Run at most two processes at once. Each script uses one numerical library thread. A full fresh primary profile takes a few minutes on this host. Repeated runs in the same scratch reuse completed profile points; use a fresh scratch directory for an independent rerun. The code checks the source manifest ID and baseline bundle validity before reading it. The source SHA-256 is `e7301e8e7a14cf45efe8f7653308e849192e02ff01b07061c11170cf080285c5`. The source SCI ID can locate the exact bundle after campaign relocation.

`files/primary/`, `files/eta08/` and `files/crowd08/` contain aggregate profiles, fit parameters, input hashes and arithmetic checks. `files/validation.json` gives the exhaustive test result. `files/moments.json` gives the model moment calculation. The two PNGs show the likelihood and covariance results. No external record-level data or compiled libraries are bundled. The package contains all new code, proof and aggregate evidence needed to inspect this claim. External source rights and attribution are in `files/EXTERNAL_DATA.md`.
