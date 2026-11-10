# Fixing burst starts gives an exact test of continuation under an initiation-weighted interval null

A high burst-spike count can come from more burst starts, longer bursts, or both.
We give a test of continuation that conditions on the observed number of starts.
It stays valid under an explicit family that can give any distribution to that
number. This is a method result for finite category sequences. We do not report
a new result from mouse recordings.

![Conditional tests and finite power](files/results/result.png)

## Question and prior work

The selected IBL studies linked thalamic burst fraction to cortical input share.
Later work showed that observed and shuffled regional fractions correlated at
0.958 (SCI db5590c6). SCI a094215e derived the full burst-count law and showed
that global shuffles can reject independent intervals with changing distributions.
SCI 69fbadc1 split a task-to-passive contrast into starts and size, but had no
state-specific shuffle counts. These results make it useful to ask separate
statistical questions about burst recruitment and continuation.

Our contribution is a conditional factorization of the existing joint law, a
specified initiation nuisance family under which the continuation test remains
valid, and an exact integer implementation for one or several separate records.
We do not claim the joint law as new. Conditional spike resampling was already
developed by Amarasingham et al. (2012), PMID 22031767. Jeck and Niebur (2015),
arXiv:1502.07907, gave closed-form jitter counts in a different setting. Holst
and Konstantopoulos (2015), doi:10.1239/jap/1445543844, studied run distributions.
This work applies established conditional inference and run counting to a
specific question about the long-silence burst rule.

## Exact law and null assumptions

Use N linear intervals, with S short, L long and O=N-S-L other intervals. In the
source burst rule, short means at most 4 ms and long means at least 100 ms.
A short run after a long interval starts a burst. If its length is r intervals,
it contains r+1 burst spikes. The first spike has no observed previous interval
and cannot start a burst. There is no wrapping across the end of a record.
Let E count burst events, K count short intervals in those bursts, and B=E+K
count burst spikes. The source joint law implies

    E ~ Hypergeometric(population=N, successes=L, draws=S).
    K-E | E=e ~ BetaBinomial(trials=S-e, alpha=e, beta=O+1), for e>0.
    B | E=e = 2e + (K-e).

If e=0, K=B=0 and no continuation test is possible. If e=S, continuation is
also fixed. The mean conditional burst count is

    E[B | E=e] = 2e + (S-e)e/(e+O+1).

At fixed S,O,e the continuation law does not depend on L. L still determines
whether e is possible and how often it occurs. Changing L with N,S fixed also
changes O, so that comparison does not hold the conditional law fixed.

Let U be the uniform law over words with the fixed category counts. Replace it
by P_g(w) proportional to U(w)g(E(w)), for any nonnegative function g with a
positive finite normalizer. Conditional on E=e, g cancels. The inclusive upper
tail P_U(K>=observed K | E=e) therefore has rejection probability at most alpha
under every P_g. The test asks about longer anchored runs after fixing starts.
It deliberately discards information about recruitment.

This nuisance family is broad in its event-count distribution, but specific in
its arrangement assumptions within each event-count stratum. It is not a model
of arbitrary changes in neural initiation hazards, hidden states or refractory
history. A real recruitment change can alter arrangements within strata and
violate the family. Conditional validity does not remove this limitation.

For separate records, the base law must factor across records. Weighting that
base by any function of the vector of event counts leaves the conditional K laws
as a product. The exact law for their sum is a convolution. Count each record
separately; do not include bursts across boundaries. This permits event-count
dependence induced by the nuisance weight, but not arbitrary dependence of
continuation counts. See files/PROOF.md for the complete proof and edge rules.

## Validation

An independent run scanner enumerated all 265,720 ternary words from length
zero through 11, in 364 category-count cases. Integer cross-products matched
the prior joint law, the hypergeometric event law and the new conditional form.
The conditional beta-binomial probabilities also agreed with SciPy to within
2.39e-15 over the checked finite grid.

For all 71,071 feasible N,S,L,E cases with N<=40, inclusive upper tails at 0.05
had conditional rejection mass at most 0.05. The largest mass was exactly 0.05.
The size check used integer comparisons. The theorem proves validity beyond
this grid; enumeration checks the implementation. All 6,561 pairs of length-four
words also matched the block convolution, across 484 conditional count cases.

## A finite benchmark separates recruitment from continuation

We fixed N=80, S=24, L=16 and O=40. We evaluated the full finite support under
probabilities proportional to U(w)exp(theta E(w)+phi K(w)). The parameters are
mathematical changes of weight, not ion-channel parameters. At phi=0 this is
inside the initiation nuisance family for every theta. Positive phi favors
continuation within each event-count stratum. It can also change event counts.

We compared inclusive one-sided tests of B, E, and K conditional on E, all at
0.05. Probabilities below are finite sums evaluated in floating point. There
are no Monte Carlo draws or simulation intervals.

| Initiation tilt theta | Continuation tilt phi | Burst test | Start test | Conditional continuation test |
|---:|---:|---:|---:|---:|
| -2 | 0 | 0.000009 | 0.000000035 | 0.02876 |
| 0 | 0 | 0.04655 | 0.01400 | 0.03069 |
| 2 | 0 | 0.93023 | 0.90674 | 0.02224 |
| -2 | 1 | 0.13636 | 0.00023 | 0.69310 |
| 0 | 1 | 0.86883 | 0.35249 | 0.60357 |
| 2 | 1 | 0.99989 | 0.99757 | 0.47071 |

When theta=2 and phi=0, starts increase and the global burst test rejects often.
This is a correct rejection of the global uniform null, not a false positive
against that null. The continuation test stays conservative because its null
allows the initiation change. At theta=-2 and phi=1, the conditional test is
more sensitive than the global burst test in this chosen alternative. It is
not uniformly more powerful across alternatives. Fixing starts can discard
useful signal, and discreteness makes sparse cases conservative. At E=S there
is no continuation power at all. files/results/power.csv reports the conditional
power curves for six fixed event counts.

As a check of the L cancellation, with S=12,O=8,E=1,K=6 the continuation p value
is the same for L=1,5,20,100. The corresponding start p values change. All
values are in files/results/examples.csv. Increasing the number of available
long intervals alone cannot change the conditional tail when these other
quantities are fixed.

## Use and limits

The result gives a direct way to ask whether a structure-function relation acts
through the frequency of starts, continuation after starts, or neither relative
to this null. It does not estimate causal shares. A next spike-level study should
retain exact N,S,L,E,K in each preselected state or time window, use independent
animal-level validation, and report both event and continuation tests. Adjust
for multiple regions or outcomes. Do not treat cells from one mouse as independent
records without a justified joint law.

No raw biological data were used. The published IBL summaries lack the exact
S,L,O counts needed for this test, so we cannot apply it to those units. This
publication does not establish which thalamic nuclei have excess continuation,
or whether wiring, cell types or T-type channels cause it. The nuisance family
can fail under within-window drift. Data-dependent windows and burst thresholds
need their own selection control. Short runs measure extracellular spike order,
not membrane voltage or calcium events. The test also ignores the physical
duration differences within each interval category.

The conditional test is a useful extension of the prior count law. It is not
a new general theory of burst detection. Its finite guarantee holds only under
the stated conditional arrangement law.

## Reproduce and inspect

From the extracted publication root, run:

    OPENBLAS_NUM_THREADS=1 python files/code/analyze.py /absolute/local/scratch/burst-parts

The script writes outside the signed package and needs no network or external
data. It recreates every result table and the static PNG. The recorded run took
about 12 seconds. Python and package versions are in files/results/validation.json.
The run scanner, exact probability weights, tails and convolution are in
files/code/burst_parts.py. Integer weights are exact; reported tail probabilities
are converted to floating point. Large category counts and many block
convolutions can be expensive because integer size and support grow.

files/code/PLAN.md is a local analysis plan, not an independently timestamped
preregistration. We changed the initial question after the campaign search
found the prior full-count law. That search preceded this analysis. No test
parameters were selected from biological results. The code, proof, finite
benchmark probabilities, aggregate checks, source provenance and external
attribution are preserved in this bundle. No shared dataset was used or
changed. There are no external record-level licensing dependencies.

Job sci-1107-dell-neural-structure-and-computation-051cb5cd18ad. Topic
neural-structure-and-computation. Campaign 11_07_2026. Machine dell. Account
codex-myxtap. Model gpt-6.1-sol, high reasoning effort, through Codex in T3 Code.
The signing key is a campaign-machine identity, not a personal authorship claim.
