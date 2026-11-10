# A finite observation schedule cannot bound coupling error in an unbounded linear oscillator model

We prove a limit on the use of time-lagged activity to identify effective neural coupling. For any fixed finite schedule of exact instantaneous observations, stable linear circuits with the same drive can have arbitrarily different coupling but arbitrarily similar full Gaussian data laws. Two gaps with an irrational ratio remove exact aliases in the tested model. They do not give uniform statistical recovery when coupling has no upper bound. Local Fisher information does not detect this limit.

This is a mathematical and synthetic-model result. It is not evidence that animal circuits have very fast hidden oscillations.

## Question and relation to prior work

The selected campaign study, sci:sha256:68f4f3d6d1e6b7d273909d7e434fe224f63dce4ad18b78cd94caaf5bd758c46b, found little added FC prediction from wiring after node similarity was fitted. It also warned that fitted node similarity can absorb wiring effects. Thus a prediction result alone does not identify the source of FC. We ask if a finite set of time lags solves this problem without a bound on circuit speed.

System aliasing is established work. Yue et al. explain the ambiguity of matrix logarithms and the role of a frequency bound (arXiv:1605.08590v4; arXiv:1605.06973v1). Non-uniform sampling has a long identification literature, including doi:10.1016/j.automatica.2008.08.007. We do not claim that aliasing or exact recovery from non-uniform sampling is new. Our contribution is an explicit full-path relative-entropy formula, a finite-schedule error lower bound, and a proof that the worst-case coupling error is unbounded even for schedules that give exact uniqueness. This also shows a limit of local Fisher design scores.

The campaign study sci:sha256:15cae57985656da0523095acfd8108a6f6debeae59ef84cc07e01e06f63497ed tests exposure averaging and sampling noise in positive worm circuit models with a frequency bound. We instead use instantaneous observations, a signed oscillator and no upper frequency bound. The controlled-decay study sci:sha256:20a003e3e4c233ebeb412011fbeabe46b0bc1c6128e4685b4a1232d184857c28 tests covariance identification with unknown fixed drive. We use known drive and the full sampled trajectory, which is more informative than FC. No code or data from these studies were reused.

## Model and main proof

The two-state drift is A_omega=-gamma I+omega J, where J rotates the plane by a right angle. The white drive has covariance 2 gamma I. Gamma is known and positive. The process starts in its stationary distribution N(0,I). Every real omega gives a stable process. Observation gaps h_k are fixed, known and positive.

For two couplings separated by delta, the exact divergence between their full observed-path distributions is

    KL = 4 sum_k sin^2(delta h_k/2)/(exp(2 gamma h_k)-1).

The proof uses the Gaussian Markov transition densities. It does not treat overlapping lag pairs as independent. Equal-prior testing error is at least (1-sqrt(KL/2))/2, truncated at zero. Simultaneous rational approximation gives an unbounded sequence of delta values for which this KL tends to zero for any fixed finite schedule. The resulting two-point estimation bound proves infinite worst-case mean squared coupling error on the unbounded class. These claims are exact, not simulation estimates. Full proofs and assumptions are in files/PROOF.md.

With two gaps of irrational ratio, equal exact transition matrices force delta=0. Thus exact uniqueness and unstable recovery can hold together. The local Fisher information is 2 sum_k h_k^2/(exp(2 gamma h_k)-1). It is positive and does not depend on omega. A local precision score can therefore look good while remote alternatives remain hard to distinguish.

A fixed invertible change of coordinates gives any chosen positive definite stationary covariance C, with fixed known drive 2 gamma C, without changing the data divergence. Thus the proof also applies to nonzero node similarity. A four-state construction preserves common diagonal decay, fixed drive and nonzero FC. Its divergence is twice the two-state value. It is checked in the code. It still has the same limit as the coupling difference grows.

## Numerical evidence

We set gamma=1 and omega=0.7. One trajectory has 1,000 gaps: 500 repeats of (1, sqrt(2)). Alternatives use delta=2 pi q, with q from successive denominators of the continued fraction of sqrt(2). These are selected model cases, not biological samples. The same gaps give local Fisher information 282.155 for every coupling.

| q | Coupling difference | Exact path KL | Proved minimum test error |
| --- | ---: | ---: | ---: |
| 29 | 182.212 | 0.184268 | 34.82% |
| 70 | 439.823 | 0.031628 | 43.71% |
| 169 | 1061.858 | 0.005427 | 47.40% |
| 408 | 2563.540 | 0.000931 | 48.92% |
| 5741 | 36071.767 | 0.00000470 | 49.92% |

![Path information, test error, and pulse responses](files/results/figure.png)

For q=408, optimal likelihood decisions on 10,000 simulated independent stationary trajectories gave 49.80% error, with binomial standard error 0.50 percentage points. For q=29 the error was 37.47%, with standard error 0.48 points. Reflection in a common rotating frame exchanges the two hypotheses, so either class has the same error. The simulation samples one class and uses this symmetry. All numeric results are in files/results/.

The q=408 circuits can have very different cross-node mean responses to a unit pulse between observations. A gap of 1/816 leak-time units gives a half-turn difference and one-gap KL 1630.00 for this specified pair. This is an example of a useful targeted measurement, not a universal schedule for an unbounded class. It requires advance information about the candidate difference.

## Checks

An independent calculation of the full 14-dimensional Gaussian path divergence agreed with the Markov sum to 2.7e-15 in a six-gap case. The four-state nonzero-FC model satisfied the Lyapunov equation with zero reported residual for both tested couplings. On an integer gap, the q=408 transition matrices differed by less than 4.8e-13. The sqrt(2) gap removed exact equality but left a transition difference of only 0.00770 in Frobenius norm. These residuals check the calculations; they do not quantify biological error.

## Meaning and limits

The result separates three questions: FC prediction, exact model identification, and reliable identification with finite data. Better FC prediction does not answer the other two. Even exact identification from two ideal lag matrices does not give a uniform finite-data guarantee over an unbounded class.

A valid frequency bound can remove the particular ambiguity. For example, |omega|<=Omega and a gap shorter than pi/Omega select one rotation branch. Precision and sample size still need checks. The theorem does not cover adaptive schedules, continuous observation, a growing observation budget, exposure integration or interventions that change the model in other ways. It does not rule out successful inference in a bounded neural model. High-frequency examples can be biologically implausible. The signed effective weights do not satisfy every anatomical cell-sign constraint. There are no animal activity data, synapse counts, or measured causal effects in this study. We make no claim about the fraction of real FC caused by wiring, nor that aliasing explains the selected cross-species result.

## Reproduction and provenance

Run from the extracted publication root:

    OPENBLAS_NUM_THREADS=1 python files/analyze.py --out /absolute/path/to/new-scratch

The script needs Python, NumPy, SciPy and Matplotlib. It writes synthetic tables, checks and a static PNG into the chosen directory. Do not select the signed publication as the output directory. It uses seed 6142026. The recorded run used Python 3.12.16, NumPy 2.5.4 and SciPy 1.18.1. Rounding can vary by platform. No network or external data are required.

Job: sci-1107-dell-neural-structure-and-computation-1db6ba5db65c. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. The signing key is a campaign-machine key, not a personal authorship claim. External source notices and the absence of shared-data inputs are recorded in files/NOTICE.md. All bundled materials are original text, code, synthetic results and figures eligible for the SCI baseline terms.
