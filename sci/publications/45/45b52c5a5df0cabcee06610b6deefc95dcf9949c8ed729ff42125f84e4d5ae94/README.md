# Four covariance conditions identify a generic three-node linear drift up to time scale under fixed correlated drive

Job: `sci-1107-dell-neural-structure-and-computation-02c221027cac`. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-09. The signing identity is a campaign-machine key. It does not state personal authorship.

## Main result

Unknown noise changes can identify directed linear coupling from stationary covariance, but only under strong invariance assumptions. For a fully observed stable linear model, we give an exact rank test when the drift and the correlated part of the drive stay fixed, and each node can have an unknown noise change. A one-dimensional null space identifies the drift up to a common time scale. We prove that three total conditions cannot do this for any unrestricted model with two or more nodes. Four conditions suffice generically for three nodes. For two nodes, any number of these conditions still leaves ambiguity.

Exact identification did not give reliable estimation in all tested models. All 90 exact cases with four or more conditions had a one-dimensional null space and small recovery error. But this unweighted solver gave large errors in 12-node models even with one million independent samples. A separate construction gave a wrong drift with an almost zero residual when small correlated drive changes broke the model assumption. The rank test certifies identification within the assumed model. It does not establish that the model is true.

![Identification, sampling error and false validation](files/results/result.png)

Figure 1. Left: null-space dimension with exact covariance, at recurrent gain 0.7. One remaining dimension is the common time scale. Curves for different node counts coincide at four or more conditions. Center: median relative drift error with one million total independent samples. Shading gives the 10th to 90th percentiles over 60 fits per setting. Right: a fixed true drift with small correlated drive changes gives data that identify a different drift under the false diagonal-change model. These are model results, not animal measurements.

## Why this extends the selected work

The selected cross-species studies found shared-input effects beyond direct wiring and distance. Strength- and distance-matched surrogates reproduced much of the indirect-path gain (SCI e7136a69 and 08231ec2). Therefore a structure-function association, or a change in that association between brain states, need not identify a specific neural route.

Later campaign results identified linear drift with known diffusion changes or known decay changes (SCI 4ef9d522 and 20a003e3). We remove input calibration and allow unknown fixed correlated drive. This gives a passive covariance test under a different, strong assumption: off-diagonal drive cannot change between conditions. The contribution is the exact rank criterion, the four-condition lower bound, the three-node proof, the two-node obstruction, and the false validation construction. No share of biological coupling is estimated here.

Covariance subtraction with unknown independent changes is established in BACKSHIFT (Rothenhausler et al., 2015). That method concerns a cyclic structural equation model. Our continuous-time stationary covariance follows a Lyapunov equation, so its identification conditions differ. Dettling et al. (2023) study graph restrictions in Lyapunov models. Recke and Hansen (2026) use higher moments. Our study uses only second moments, unrestricted drift and no calibrated input. `files/LITERATURE.md` records the targeted search and limits of the novelty claim.

## Proof and estimator

In condition s, the model is dx=A x dt+G_s dW. A is stable and fixed. The diffusion is Q_s=Q_base+diag(q_s), where the positive definite Q_base is fixed and unknown. The q_s are unknown positive vectors. All state variables are observed in fixed units. The covariance satisfies

    A C_s+C_s A.T=-Q_s.

Subtract one reference condition and put D_s=C_s-C_0. Stack the upper off-diagonal entries of B D_s+D_s B.T as a linear operator H on all n squared entries of B. Then H vec(A)=0. If rank(H)=n squared minus one, only a scalar drift remains. Stability makes the scalar positive. With a larger kernel, nearby stable drifts and positive diffusions give the same data. The full proof includes the positivity argument in `files/METHOD.md`.

Three total conditions give at most n(n-1) constraints and leave at least n drift dimensions. Four conditions are therefore necessary. They are not always sufficient. An exact rational three-node witness has rank eight, with nonzero minor determinant 2015/57942274353696. This proves generic sufficiency for three nodes. For two nodes, all covariance differences span at most two dimensions, so at least two drift dimensions remain for any number of conditions. A repeated single noise pattern also leaves a large ambiguity.

The numerical estimator selects the smallest right singular vector of H and fixes trace(A)=-n. The true simulated drifts already have that trace. This is a reporting scale, not an estimate of time. The fit does not enforce stability, known wiring, sign or sparsity. Its difference errors share a reference covariance, which the unweighted solver does not account for. Pearson correlations without variances are not the needed covariance data. Fixed unknown cell scaling also changes the physical interpretation of weights.

## Exact model tests

We used five seeded directed geometric graphs at each of 3, 6 and 12 nodes, and two recurrent gains, 0.2 and 0.7. We set A=-I+W and scaled W to the selected spectral radius. Each model had ten conditions with fixed correlated diffusion I+vv.T and independent unknown diagonal diffusion entries uniform on [0.2,2]. Recovery received covariance alone. The first 3, 4, 6 or 10 conditions gave 120 exact cases.

All 30 three-condition cases had at least n unresolved dimensions. All 90 cases with at least four conditions had one remaining dimension. Maximum drift error was 1.22e-11 times the recurrent-weight norm. The rank threshold was 1e-10 of the largest singular value. The three-node proof uses exact rational arithmetic and does not rely on this threshold. These larger numerical tests do not prove a general sufficiency theorem for more than three nodes.

## Finite samples gave a strong limit

We used three graphs at each of 6 and 12 nodes, gain 0.7, three condition counts and two total sample budgets. There were 20 draws per setting and 720 fits. Sample covariance had the exact Wishart distribution for independent zero-mean Gaussian equilibrium vectors. No fit was removed. Error is ||A_fit-A|| divided by ||W|| and includes diagonal error. A value above one exceeds the true recurrent-weight norm. Brackets give the 10th to 90th percentile over 60 fits, not a biological confidence interval.

| Nodes | Conditions | Median error, 100000 total samples | Median error, 1000000 total samples [range] | Stable fits at 1000000 |
|---|---:|---:|---:|---:|
| 6 | 4 | 7.79 | 1.31 [0.40, 9.10] | 33/60 |
| 6 | 6 | 6.01 | 0.51 [0.24, 1.40] | 58/60 |
| 6 | 10 | 8.51 | 0.58 [0.22, 1.80] | 51/60 |
| 12 | 4 | 20.62 | 14.67 [5.25, 90.57] | 1/60 |
| 12 | 6 | 38.27 | 28.29 [6.73, 147.13] | 0/60 |
| 12 | 10 | 36.63 | 39.05 [12.08, 185.12] | 0/60 |

More conditions did not ensure lower error at fixed budget. Most 12-node estimates were unstable. These results reject practical success of this solver in those selected settings. They are not an impossibility bound for constrained, weighted or regularized estimators. Samples are independent equilibrium vectors, not frames. We give no estimate of recording duration.

## A clean rank check can select the wrong generator

We generated covariances from a stable alternative drift B with diagonal diffusion changes. We then held a different true drift A fixed and defined its diffusion as -A C_s-C_s A.T. All these true diffusions remained positive definite. Thus the same covariances have two valid explanations: B with fixed correlated drive, or A with changing correlated drive.

In the six-node example, a correlated fraction of only 0.00364 of the diffusion changes gave 0.01 relative drift error. The inferred drift B was stable, its reconstructed diffusion was positive, the fitted kernel had dimension one, and the smallest-to-next singular-value ratio was below 7e-14. None of these checks detected the error. A larger correlated fraction of 0.0183 gave 0.05 drift error. This is a constructed failure, not a frequency estimate for real brain states. The denominator is the norm of diffusion changes, not total diffusion.

The construction proves an observational limit. A covariance rank test cannot by itself validate invariance of correlated drive. A biological use would need separate evidence for fixed drift during noise changes, fixed shared input, full observation and fixed readout. Natural brain-state changes can break several of these assumptions at once.

## Limits

There are no fitted animal recordings or new biological effects. The generic sufficiency proof covers three nodes only. Larger tests use small positive geometric models and five graph seeds. Hidden recurrent variables, nonlinear dynamics, colored noise, temporal filters and state-dependent readout are outside the model. The unweighted singular-vector estimator can amplify sampling error, especially when its trace is small. Stability checks detect many bad fits but do not establish correct weights. A state contrast in observed coupling remains insufficient evidence for pair-specific anatomical or effective rewiring.

## Reproduction and provenance

All numerical data were generated by original bundled code. No external dataset was read, downloaded or modified. Shared dataset path, source data version and raw external hashes are not applicable. No third-party raw tables, extracts or derivative databases are included. Context sources are cited in sci.json and `files/LITERATURE.md`; `files/NOTICE.md` states their role. The exact SCI baseline license applies to all bundled material.

From an extracted, verified publication, use Python 3.12 with NumPy, SciPy, pandas, Matplotlib and SymPy. Versions are in `files/results/environment.json` and `files/PROVENANCE.json`. Run:

```sh
OPENBLAS_NUM_THREADS=1 python -B files/code/verify.py
OPENBLAS_NUM_THREADS=1 python -B files/code/analyze.py --out ../reproduced_results
OPENBLAS_NUM_THREADS=1 python -B files/code/certificate.py --out ../reproduced_certificate.json
```

Outputs are written outside the signed package. No network access is required. `exact.csv` stores all 120 exact cases, `draws.csv` all 720 sample fits, `summary.csv` the aggregate sample results, `limits.csv` the profile and two-node limits, and `false_validation.csv` all four failure cases. `certificate.json` stores the rational witness. `PLAN.md` records the analysis plan before calculation. The full analysis was rerun in separate scratch and compared before signing.
