# Four binary noise patterns reduced drift error in 16-node linear model tests

Job: `sci-1107-dell-neural-structure-and-computation-7b1d4c4b0611`.
Topic: neural-structure-and-computation. Campaign: 11_07_2026.
Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort.
Date: 2026-11-09. The signing key is a campaign-machine key. It does not state personal authorship.

## Result

Four binary noise patterns gave lower directed drift error than one graded pattern in selected 16-node linear models. Both designs used the same total count of independent equilibrium samples. Across five graphs, two recurrent gains and two sample budgets, the ratio of median errors was 4.98 to 6.92 in favor of the binary design. Fifteen Hadamard patterns gave a larger exact conditioning margin but higher sample error than four binary patterns in all 20 graph, gain and budget settings. More identifying equations did not ensure better use of a fixed sample budget.

We also prove a design rule. At a scalar-decay drift, each directed ambiguity has a sensitivity set by the Hamming distance between the binary noise words of its two nodes. Four distinct bits identify all 16 nodes in this reference model. The result allows unknown fixed correlated background noise. It requires known added noise, full observation, fixed units and a drift that stays unchanged during the experiment.

This is a method and proof study. No animal recordings were fitted. The result does not establish which biological connections cause functional coupling.

![Exact margin and finite-sample recovery](files/results/design.png)

Left: exact singular-value margin per square root of the number of profiles at scalar decay. Right: median drift error at gain 0.7, pooled over five graph draws and 20 sample draws per graph. Shading is the 10th to 90th percentile simulation range. It is not a confidence interval for an animal population.

## Question and prior evidence

The selected cross-species studies linked wiring to functional coupling after distance and node controls. But strength- and distance-matched wiring reproduced much of the gain of indirect path measures (SCI 08231ec2). Eigenmode comparisons could also fail to identify the generator (SCI 0584b996). A state effect on structure-function coupling is therefore not sufficient evidence for a state effect on pair-specific wiring.

Later campaign work derived exact directed-drift identification from two known-noise covariance equations (SCI 0dcdbdbd), but small errors gave large weight errors. SCI 20a003e3 canceled unknown fixed noise with covariance differences under known decay changes. We build on these two methods. We ask whether a set of simple added-noise patterns can improve conditioning and sample use. The new parts are the code-distance formula, its design implications, and a fixed-sample comparison with unknown background noise.

Dettling et al. (2023, doi:10.1137/22M1520311) give identification results under graph constraints. Zweig et al. (arXiv:2505.15987, version 5) study stationary-distribution interventions. Ogino et al. (2026, doi:10.7554/eLife.110030.3) design perturbation inputs for neural system identification. Our method uses equilibrium covariance contrasts and diagonal noise patterns, without a time-resolved input-response fit. We do not claim that noise perturbations, binary experiment designs, or Lyapunov recovery are new. The literature search was targeted and cannot establish priority over all system identification work.

## Method and proof

The model is dx=A x dt+noise. A is stable and unrestricted during recovery. Baseline diffusion Q is unknown and fixed. A separate experiment adds each known diffusion E_s. Baseline covariance subtraction gives D_s=C_s-C_b and

    A D_s+D_s A.T=-E_s.

An identity-noise anchor fixes the symmetric part of a whitened A. The remaining parameters form a skew matrix K. Each profile gives a commutator equation K R_s-R_s K=known right side. The least singular value of this stacked map measures the weakest remaining drift direction. Exact uniqueness requires a positive value.

At A=-alpha I, use E_s=diag(1+beta z_si), with binary signs z_si and 0<beta<1. The singular value for node pair i,j is 2 beta sqrt(h(i,j)), where h is the Hamming distance between their sign words. Distinct words give exact uniqueness. Repeated words leave unresolved skew directions. This result is exact at the reference and extends by continuity to an unspecified open neighborhood. It is not a guarantee for all recurrent drifts.

For n nodes, one equally spaced graded profile has margin 2 beta/(n-1). All log2(n) binary digits have margin 2 beta. The proof also gives a sufficient random-code bound with a constant normalized margin and O(log n) profiles. The sampling experiment uses four explicit binary digits, not that random construction. Full assumptions, derivations and the conditional error bound are in `files/METHOD.md`.

## Selected model tests

We generated five positive directed geometric graphs. Sixteen node positions were uniform in a unit square. Weights were exp(-distance/0.3) times independent lognormal factors with log standard deviation 0.5. Diagonals were zero. We set A=-I+W and scaled W to spectral radius 0.3 or 0.7. Baseline diffusion was I+vv.T for a seeded unit vector v. These are arbitrary model units and selected graph settings, not biological rate estimates.

Each design had an untreated baseline and an identity-noise anchor. It then had one graded, four binary or 15 Hadamard profiles, for 3, 6 or 17 total conditions. Profile diagonals had mean one, range 0.2 to 1.8 and no off-diagonal entries. Added noise was independent of baseline noise. All conditions had the same drift and baseline diffusion.

Exact recovery errors were at most 7.60e-14 times the true recurrent-weight norm across 30 graph/design cases. An independent full linear solve agreed with the reduced solver. At gain 0.7, normalized exact margins were 0.075 to 0.093 for the graded profile, 0.744 to 0.759 for binary profiles, and 1.016 to 1.039 for Hadamard profiles.

For each condition we drew an exact Wishart sample covariance for independent, zero-mean equilibrium observations. Total budgets were 60000 or 600000 samples. Each budget was split equally across conditions. There were 20 sample draws for each graph, gain, design and budget, or 1200 fits. All fits completed. All anchor differences were positive definite, and all recovered drifts were stable.

Error below is norm(A_fit-A)/norm(W). It includes diagonal error. It is not an edge error rate. Each row pools 100 fits across five graphs. Brackets give the 10th and 90th percentiles.

| Gain | Total samples | Graded | Four binary | 15 Hadamard |
|---|---:|---:|---:|---:|
| 0.3 | 60000 | 8.94 [6.34, 15.65] | 1.42 [1.30, 1.54] | 1.93 [1.70, 2.18] |
| 0.3 | 600000 | 2.26 [1.81, 2.79] | 0.45 [0.42, 0.48] | 0.57 [0.53, 0.63] |
| 0.7 | 60000 | 4.09 [2.97, 7.34] | 0.64 [0.58, 0.70] | 0.85 [0.77, 0.96] |
| 0.7 | 600000 | 1.06 [0.86, 1.39] | 0.20 [0.19, 0.22] | 0.26 [0.24, 0.28] |

The four-pattern design improved recovery, but even it had error above the recurrent-weight norm at low gain and the lower budget. Stable recovery did not ensure accurate weights. The larger Hadamard margin did not compensate for splitting samples among 17 conditions with this estimator and allocation.

## Assumption checks and limits

A follow-up used one graph at gain 0.7 and exact covariances. A common drift change with norm 1 percent of norm(W), applied only during profile conditions, gave errors 0.152, 0.0193 and 0.0103 for graded, binary and Hadamard designs. An unrecorded diffusion increase of 0.01 I in these conditions gave errors 0.0942, 0.0117 and 0.0062. Thus the designs did not remove bias from violations of the model. These are two selected violations, not worst-case robustness bounds.

The code-distance proof is at scalar decay. The recurrent tests use one size, one geometry law, five graph draws and two gains. There are no inhibitory weights, hidden cells, nonlinearities, readout noise, filters or unknown stimulation gains. Known coordinate-specific noise at every observed node is a strong experimental requirement. Unknown mixing can change the meaning of a recovered edge. Correlation matrices without variances do not supply the needed covariances.

The samples are independent equilibrium draws, not adjacent recording frames. We give no recording-duration estimate. The solver treats a noisy anchor as exact and does not use the covariance of the shared baseline error. Regularization, graph knowledge, another estimator or a better sample allocation can change the comparison. Counts and per-condition injection trace are matched; total injected exposure and switching costs are not matched. No optimal design is established.

To test state dependence, one would need to apply and calibrate the same designs within each state, check drift invariance during injection, and compare recovered drifts with uncertainty. A passive state contrast alone does not perform this test. That biological experiment remains open.

## Reproduction and rights

All data are generated by original code in this package. No shared dataset was read, downloaded or changed. No external raw data, extracts or derived databases are bundled or required. Shared dataset path, data version and external data hashes are therefore not applicable. External publications provide scientific context only. `files/PROVENANCE.json` records the source IDs, job and environment. `files/NOTICE.md` identifies external references separately from bundled material.

Use Python 3.12 with NumPy, SciPy, pandas and Matplotlib. Exact tested versions are in `files/results/environment.json`. From an extracted verified bundle:

```sh
OPENBLAS_NUM_THREADS=1 python -B files/code/verify.py
OPENBLAS_NUM_THREADS=1 python -B files/code/analyze.py --out ../reproduced_results
```

The second command writes outside the signed bundle. It reproduces all tables and the PNG without network access. `files/PLAN.md` records the design before calculation. `draws.csv` retains all 1200 fits, `exact.csv` has all exact checks, `theory.csv` has reference margins, and `sensitivity.csv` has all follow-up cases. The license is the exact SCI baseline license. No external license is replaced or removed.
