# Equal delay means and variances gave different gain limits in 91 selected Allen mouse pair models

Two delay laws with equal mean and variance gave different stability limits in all 91 selected mouse circuit models. The law with equal mass at zero and twice the mean gave a critical feedback gain 7.51% lower at the median than an exponential law. The range was 1.91% to 10.86% lower. A difference above 5% occurred in 69 pairs; a difference above 10% occurred in eight pairs. Thus, matching two delay moments did not keep gain error below 5% in most of this sample.

These are model results. No delay distribution, firing-rate gain, stability transition, or brain oscillation was measured. The contribution is a reproducible benchmark and a finite branch search, not a new general claim that delay shape affects stability.

![Gain limits with matched delay moments](files/figure.png)

## Question and prior work

How much can critical gain change when a model keeps the first two moments of total feedback delay but changes its shape? Allen circuit records link reciprocal chemical connectivity to response onset and decay in the same cells. We use these records to set model time scales, not to estimate a biological delay distribution.

Campagnola, Seeman and colleagues provide the source experiment (doi:10.1126/science.abj5861). Meyer and colleagues studied distributed delays in neural feedback (arXiv:0712.0036). Jessop and Campbell studied stability approximation with delay moments and cumulants (doi:10.1016/j.neunet.2010.06.009). The role of distribution shape beyond its moments is established context. The present contribution is its size in a defined linked-data benchmark, with a complete search for the first loss of stability.

We searched the campaign with `sci search` for `connectome`, `non-normal`, `electrical`, `delay`, and `delay kernel` before the numerical test. We read publication sci:sha256:0d12049772a595bb27ce0fd1c1cdc190f1aab31df8b22da60df162eb4e450266, which compared fixed delay with Erlang chains in this same sample. That test changed variance. Our test keeps both mean and variance fixed. We follow its sample definition and model-filter convention, but write new code and query the source again. The earlier publication's record extracts are not reused or bundled. Search was targeted, not an exhaustive novelty review. files/design.md records the design before numerical analysis. This is an exploratory study, not a preregistered test.

## Data and linkage

The input is Allen Synaptic Physiology r2.1 small, file dated 2023-01-26. Its exact shared path, source URL, size and hash are in files/provenance.json and files/EXTERNAL_DATA.md. The SHA-256 is `7372499fdd874f057565080d5769baaf2659ef39d9f3bc3c7147dd1e1c280a53`. We opened the database read-only. No download was needed.

The SQL in files/analyze.py joins pair, synapse, both cell records, experiment and slice. It starts with detected chemical connections. A pair must have both directions in one experiment: one excitatory and one inhibitory. Both nonsynaptic cell labels must agree with these signs. Both onset latencies and both voltage decay times must be finite and positive. We count each E-I pair once, from its excitatory direction. Linkage uses exact cell and experiment IDs, with no cross-animal alignment.

Mouse VisP has 302 reciprocal E-I pairs, 142 with consistent labels, and 91 with complete positive times, in 77 recordings. Human TCx has 23 reciprocal pairs, eight with consistent labels, and three with complete times. The 91-pair count matches the earlier campaign study. We make no independent-animal sampling claim and do not infer donor identity. Human data are a descriptive scope check. Species and region cannot be separated.

Stored latency is onset time relative to the source spike reference. The sum of both latencies defines D. It is not a measured mean of a distribution of loop delays. Voltage decay times define a and b. They include membrane and recording effects and need not be neuronal rate-response filters. A positive stored fit is not a validated estimate. We do not refit traces or select on fit residuals. An interior-decay check removes values outside the open interval (0.00501, 0.499) seconds; it is an endpoint check, not fit quality control.

## Models and exact calculation

Both models have loop transfer `K H(s)/P(s)`, with negative feedback and

`P(s) = (1+a s)(1+b s)`.

K is a nonnegative static loop gain. It is not inferred from voltage amplitude. The characteristic equation is `P(s)+K H(s)=0`. There are no other cells, self-links, rise filters, nonlinearities, thresholds, adaptation or behavioral inputs. H represents the total loop delay law, not two independently sampled edge delay laws.

The exponential law has density `exp(-t/D)/D` for t >= 0 and transform `H_E(s)=1/(1+D s)`. The two-point law has probability 1/2 at t=0 and probability 1/2 at t=2D, with transform `H_B(s)=(1+exp(-2D s))/2`. Both have mean D and variance D squared. Their third raw moments differ: 6D cubed and 4D cubed. The zero-delay atom is deliberate. These laws are mathematical alternatives, not fitted transmission distributions.

The exponential model is a cubic polynomial after multiplication by (1+D s). Its Routh-Hurwitz boundary is

`K_E = [ab+D(a+b)](a+b+D)/(abD)-1`,

`w_E = sqrt[(a+b+D)/(abD)]`.

For the two-point model, let `theta(w)=atan(a w)+atan(b w)`. Its candidate imaginary roots satisfy

`theta(w_m)+D w_m=m pi`, for positive integers m.

This phase equation has one positive root for each m because its left side increases strictly. To see which roots have positive K, write `H_B(iw)=cos(Dw) exp(-iDw)`. At a phase root, a positive K requires `theta(w)>pi/2`, or `ab w squared > 1`. Each valid root gives

`K_m = [(1-ab w_m squared) squared + w_m squared (a+b) squared] / (ab w_m squared - 1)`.

We take the smallest K_m over all valid m. We do not assume that the first frequency branch gives the smallest gain. The finite stopping rule is exact: `K_m >= ab w_m squared - 1`, and w_m increases with m. Once this lower bound exceeds the best gain, no later branch can improve it. The code uses dimensionless time for conditioning.

At K=0 both models are stable. At s=0 the characteristic value is 1+K, so no nonnegative gain gives a zero root. For K in a bounded interval, an unstable root cannot arrive from infinite frequency: in the closed right half-plane, |H_B| <= 1 and |P| grows without bound. Thus the minimum positive imaginary-root gain is the boundary of the stable interval that starts at K=0. Numerical root checks confirm a crossing toward instability at the selected minima. No claim is made about stability at much larger gains.

## Results

The main ratio is K_B/K_E. A value below one means the exponential model permits a larger stable interval from K=0 than the two-point model.

| Mouse selection | Pairs | Median ratio | Full ratio range | Absolute difference above 5% |
|---|---:|---:|---:|---:|
| Primary | 91 | 0.92493 | 0.89137 to 0.98088 | 69 |
| Interior decays | 64 | 0.92918 | 0.89621 to 0.98088 | 51 |
| Half onset delays | 91 | 0.95575 | 0.91656 to 0.99012 | 36 |
| Twice onset delays | 91 | 0.89815 | 0.87142 to 0.97622 | 85 |

The interior sample spans 57 recordings. With twice the delays, 50 of 91 ratios differ by more than 10%. With half the delays, none does. Both laws still have equal means and variances within every sensitivity comparison. Complete aggregate results are in files/summary.csv.

All three selected human ratios were below one, with median 0.93421 and range 0.92823 to 0.94959. Three records cannot establish transfer across species or regions. No confidence interval or population p value is reported. The quantities are deterministic summaries of selected stored fits under stated model assumptions. Uncertainty in those fits and missing-data selection is not propagated.

The primary direction is not a universal law. A synthetic grid of a,b,D in {0.1,1,10} had two of 27 cases with K_B/K_E above one. These two cases exchange a and b and are the same case up to cell order: a=0.1, b=10, D=1 gives ratio 1.02683. Thirteen grid cases required a branch above one; the largest selected branch was 56. This check shows why a first-branch assumption can fail outside the data scope. The synthetic table contains no third-party values.

## Validation and limits

The calculation checks the characteristic residual and solves nearby complex roots at 0.999 and 1.001 times each threshold, for 282 model cases (94 pairs at three delay scales), plus 27 synthetic cases. The largest scaled residual is 2.59e-12. It checks exchange symmetry and uniform time scaling. For every synthetic case, an additional scan of 100 phase branches agrees with the finite-bound answer.

A separate script uses bisection and direct complex division for all 282 data-based cases. It also checks the cubic identity and rules out every branch after the first with the next-branch lower bound. Its largest relative gain difference is 8.54e-13. Both scripts stop on failed assertions. files/checks.json and files/independent_checks.json preserve the reports. These are numerical checks, not validated physiological dynamics.

The two laws differ in skewness, tail behavior and support, as well as higher moments. We do not isolate one of these causes. In particular, the two-point law places half its mass at zero. Matching mean and variance does not make this law biologically plausible. A narrow positive-delay distribution could give a different result. The stored onset is not a measure of delay variance. Unit-area voltage filters and a static gain product are strong assumptions. Missing fits, cut axons, selected cell types and unmeasured circuit inputs limit transfer. No activity dataset, intact circuit stability, behavior or representation reliability was tested.

The practical use is a stress test for model reductions: a two-moment match alone did not certify a 5% gain-limit tolerance for these chosen alternatives. Measured delay kernels and appropriate response filters are needed before this result can support an intact-brain prediction.

## Reproduction

The bundle has original code, aggregate model findings, synthetic evidence, the figure, and exact input provenance. Raw data and all record-level tables stay outside the bundle because of source terms. No private scratch is needed once the external source is available.

From a local copy of the publication, use Python with files/requirements.txt (versions used are also in provenance). Set an output directory outside the publication, then run:

```sh
python files/analyze.py --db /mnt/dell-data/shared_datasets/allen-synphys-r2.1-small-20230126/synphys_r2.1_small.sqlite --out ../reproduced
python files/verify_numeric.py ../reproduced
```

The input hash is mandatory. The first command writes regenerated external_records.csv, summaries, checks, provenance, synthetic cases, and the figure into that external directory. Never copy external_records.csv into a signed draft. Compare summary.csv and synthetic.csv with the bundled files. If the source is unavailable, use `python files/retrieve.py ../external_input` and pass the returned path to --db. Retrieval writes only outside the publication. Respect Allen terms; read files/EXTERNAL_DATA.md. On this campaign, reuse the existing shared source. An unavailable shared mount is a blocker, not a reason to create a replacement directory.

## Job and rights

Job: sci-1107-dell-neural-structure-and-computation-4bde1f5b6b6e. Topic: neural-structure-and-computation. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort, Codex harness through T3 Code. Date: 2026-11-09. No agents were launched. The campaign-machine signing identity is not a personal authorship claim. No key is bundled. The signed ZIP is saved locally, with no remote upload or submission.

Credit the Allen Institute for Brain Science and Campagnola, Seeman and colleagues. The exact SCI baseline LICENSE applies to original bundled materials. The external database and regenerated records have their own source terms and are not included. The separate external-data notice records attribution, terms and retrieval details.
