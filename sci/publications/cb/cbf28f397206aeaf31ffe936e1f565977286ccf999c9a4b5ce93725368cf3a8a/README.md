# Noise contrasts give a sample-based drift error bound with unknown fixed input and readout noise

Job: sci-1107-dell-neural-structure-and-computation-4f3f8c3a4cad. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through the Codex harness in T3 Code. Date: 2026-11-10. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question and main result

Can controlled noise reveal directed coupling when both background drive and readout noise are unknown? We give a sample-based error bound for a fully observed stable linear stochastic system. Known added process noise changes the covariance. Drift, background process noise and readout noise must stay fixed. Subtraction of a measured baseline removes both unknown noise covariances. A full linear operator then tests which drift directions the experiment can separate.

The new method combines measured operator sensitivity with a Gaussian covariance bound. It uses measured covariance matrices, independent sample counts and a chosen failure probability. It does not need the true covariance error or an exact baseline. It returns a confidence ball for the full directed drift, or an infinite radius when the evidence is too weak. The same method allows unknown correlated readout noise that is independent of the latent signal and fixed across conditions.

This is a proof and synthetic method study. We did not fit neural recordings or re-estimate the cross-species wiring gains. Effective drift is not a synapse count. The result gives a testable route from passive FC to causal experiments under explicit model assumptions. It does not explain the biological node-similarity structure.

## What this adds to prior work

The selected campaign work found reliable functional connectivity (FC), but later controls showed that surrogate comparisons and eigenmode advantages can fail to identify its generator. We follow the causal branch of that objective. The small held-out wiring gains do not by themselves bound causal coupling.

Campaign study 4ef9d522 used covariance contrasts and binary noise patterns with unknown fixed process noise. Study d5d44b56 gave a finite probe-error bound with a known exact baseline and the true covariance error. Our extension removes those two uncertainty restrictions and allows fixed unknown readout noise. We use the full drift operator rather than treating a noisy whitening transform as exact. This also accounts for reuse of the same uncertain baseline in every contrast. We do not claim that covariance subtraction, noise probes, binary patterns, inverse Lyapunov equations or Gaussian concentration are new.

Dettling et al. (2023, doi:10.1137/22M1520311) study graph constraints in stationary Lyapunov models. Salehkaleybar (2026, arXiv:2609.19955v1) studies steady-state drift interventions under graph and spectral conditions. Our intervention adds known diffusion and leaves drift fixed. Rudelson and Vershynin (2010, arXiv:1003.2990v2, equation 2.3) state the Gaussian singular value inequality used in our proof. The source review was targeted. It does not establish global priority.

## Model and bound

In condition s, latent covariance C_s obeys A C_s+C_s A.T+Q+E_s=0. A is stable, Q is unknown and fixed, E_s is a known added white-noise covariance, and E_0=0. Observed covariance is V_s=C_s+R, with unknown fixed R. All coordinates are observed in fixed units. Readout noise is independent of the signal. Thus D_s=V_s-V_0 obeys

    A D_s + D_s A.T = -E_s.

Stack H -> H D_s+D_s H.T to form T. Drift is unique in these linear equations when T has full column rank. This is an existing identification criterion expressed in the full drift space. Q and R remain inseparable even when A is identified.

For each measured covariance Vhat_s based on N_s independent zero-mean Gaussian snapshots, set

    u_s = sqrt(n/N_s) + sqrt(2 log(2L/delta)/N_s),
    r_s = sqrt(n) ||Vhat_s||_2 (2u_s+u_s^2)/(1-u_s)^2.

Use infinity if u_s>=1. Jointly, all covariance errors are at most r_s with probability at least 1-delta. Let e=sqrt(sum_{s>0}(r_s+r_0)^2), let shat be the smallest singular value of the measured contrast operator, and let rho be the equation residual of a fitted Ahat. If shat>2e, then

    ||Ahat-A||_F <= (rho+2 ||Ahat||_2 e)/(shat-2e).

Otherwise report infinity. Including infinite outputs, this is a confidence ball with coverage at least 1-delta. The probability of a finite bound that misses the true A is at most delta. We do not claim 95% coverage conditional on a finite output. We set delta=0.05 for each fixed experiment. The proof is in files/PROOF.md. The procedure does not test its own model assumptions.

## Synthetic test

We used six directed positive geometric graphs: three seeds each at 4 and 8 nodes. Positions were uniform in a unit square. Weights were exp(-distance/0.3) times lognormal multipliers with log standard deviation 0.5, with no diagonal. Recurrent weights W had spectral radius 0.6, and A=-I+W. Baseline process noise was I+vv.T for a seeded unit vector v. Readout covariance was r Z Z.T/n for a fixed Gaussian matrix Z and r=0,1,10. These are arbitrary model units.

Each design used an untreated baseline, an identity-noise anchor, and log2(n) binary profiles. Profiles were diagonal with entries 0.2 or 1.8. Every increment was multiplied by dose 1 or 10. Total independent sample budgets were 10^4, 10^6, 10^8 and 10^10, split equally among 4 or 5 conditions, with integer rounding down. Thirty sample draws per setting gave 4,320 fits. Bartlett sampling generated exact Wishart-distributed sample covariances without constructing the large raw sample arrays. These counts are not recording frames or feasible neural experiment durations. The design and delta were fixed before these draws.

Readout noise canceled from the exact equations but increased sample error and the bound. Finite bounds need not be small or useful. All raw numerical results are synthetic and retained in files/results. See the result table below.

Across all 4,320 fits, 2,160 bounds were finite. No finite bound missed the true drift, and every computed covariance-error radius covered its true contrast error. These are simulation counts, not a proof of nominal coverage. The theorem gives the probability claim. Exact recovery error was at most 1.98e-14 in absolute Frobenius norm across 12 graph-dose cases. Independent Kronecker-operator and perturbation checks passed in 48 cases; rank and varying-readout controls also passed.

Finite bounds were conservative: bound/error ranged from 25.65 to 351.85, with median 72.32. At total budgets 10^4, 10^6, 10^8 and 10^10, the finite counts were 0, 180, 900 and 1080 out of 1080 fits at each budget. These counts apply to the tested grid only.

Eight-node models, dose 10 (90 fits per row):

| Readout scale | Total samples | Median relative drift error | Finite bounds | Median absolute radius |
|---|---:|---:|---:|---:|
| 0 | 1,000,000 | 0.00898 | 0% | infinite |
| 0 | 100,000,000 | 0.00090 | 100% | 0.1636 |
| 1 | 1,000,000 | 0.01122 | 0% | infinite |
| 1 | 100,000,000 | 0.00112 | 100% | 0.2143 |
| 10 | 1,000,000 | 0.03294 | 0% | infinite |
| 10 | 100,000,000 | 0.00339 | 100% | 1.3930 |

![Sample error and the computed confidence bound](files/results/certificate.png)

The first two panels show the 8-node models at dose 10, pooled over three graph seeds. Median errors use all 90 fits per setting. The last panel shows every finite bound across all settings. It compares absolute Frobenius errors and bounds. The dashed line marks equality. The plot is a simulation audit, not evidence for neural population coverage.

## An exact limit

Changing readout noise defeats the claim. With one state, A=-1, Q=1 and an added diffusion of 1 give latent covariances 0.5 and 1. Readout variances 1 and 0.75 give measured variances 1.5 and 1.75. A second model, A=-2 and Q=2 with constant readout variance 1, gives those same observations for the same increment. The fit returns -2, and its radius goes to zero with more samples. The fixed-readout assumption matters even with exact data. Unknown fixed readout and process noise also remain mutually ambiguous; only drift can be recovered by these contrasts.

## Limits

The proof needs a fixed linear drift, known added diffusion, full observation, fixed units, independent Gaussian snapshots and fixed independent readout noise. Hidden states, unknown mixing, temporal filtering, changing readout noise, stimulation-induced gain changes or calibration error can invalidate it. Correlation-only FC lacks required variances. We give no conversion from correlated neural frames to independent samples. Non-Gaussian data need another covariance bound. Data-dependent probe or stopping choices need extra probability control.

The confidence radius is conservative and controls all drift entries together. Infinity does not prove no coupling. Six small graph models do not establish performance across neural architectures. We did not optimize designs, sample allocation or estimators, and did not compare biological data. The large sample counts expose the difference between algebraic identification and a useful guarantee. The result is a method with restricted scope, not a resolution of which biological node properties generate FC.

## Reproduction and rights

All inputs and code are new synthetic material. No shared dataset was read, downloaded or changed. No external raw data, extracts, derivative databases, article PDFs or code are bundled. The exact input hash and environment are in files/PROVENANCE.json and files/results/environment.json. External context and attribution are in files/NOTICE.md. The SCI baseline license applies to bundled material.

From an extracted verified bundle, with Python 3.12, NumPy, SciPy, pandas and Matplotlib:

    OPENBLAS_NUM_THREADS=1 python -B files/validate.py
    OPENBLAS_NUM_THREADS=1 python -B files/analyze.py --out /absolute/path/to/new-local-scratch

The second command reproduces all simulation outputs and the PNG without network access. Do not write into the signed bundle. Exact matrices are in files/results/synthetic_inputs.npz, all 4,320 draws in trials.csv, grouped results in summary.csv, and exact solves in exact.csv. Small numeric or PNG differences can occur across libraries. No private scratch is required.

For a new fixed experiment, supply an NPZ with covariances (L,n,n) and increments (L-1,n,n), with equal sample counts in all conditions:

    OPENBLAS_NUM_THREADS=1 python -B files/certify.py /path/to/input.npz --n-per-condition 1000000 --delta 0.05 --output /path/to/local-scratch/certificate.json

A null radius means no finite bound. Read files/PROOF.md for all assumptions before use. The script does not infer them from data. files/PLAN.md records the exploratory plan before the main simulation.
