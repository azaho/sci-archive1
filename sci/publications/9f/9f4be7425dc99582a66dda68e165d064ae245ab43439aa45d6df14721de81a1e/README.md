# Fixed edit budgets give exact bounds on equal-side synapse count scores

## Result

A bound on the number of missed or extra synapses can give an exact range for a fixed-panel bilateral count score. The range depends on where errors can occur. Global synapse recall does not determine that range. Random audits of true paired counts can estimate the score without an independence assumption for reconstruction errors. We prove these results and supply a count-bound tool. All numerical examples are synthetic. No new animal measurement or biological error rate is reported.

The target is the mean of `(left-right)^2/(left+right)` across a fixed panel of named connection pairs, with score zero for an empty pair. This is the conditional Pearson score for equal sides, p=1/2. It is not a marginal Fano factor. It includes any systematic side difference. We do not fit neuron gains.

## Why this question matters

The selected SCI studies found low bilateral count dispersion in worms and high dispersion in flies [1]. Later work split the fly excess into constant and multiplicative parts [2], spatial and cell factors [3], and side-specific and bilateral parts [4]. A further campaign study found side-label errors and little evidence for a component shared by an imaging pipeline [5]. Another study proved that count thinning alone cannot separate anatomy from reconstruction [6]. Thus a small detector difference or a high overall recall cannot by itself settle the source of count dispersion.

We ask a narrower question that can be answered: given possible count errors, which score values remain feasible, and what audit can estimate the true score even when errors are shared?

Horvitz and Thompson established inverse-probability sampling [7]. Two-phase validation studies use related designs [8]. SynEM studied how individual synapse quality affects connection quality and stated an independence condition for combining contacts [9]. We do not claim to invent these general sampling or optimization methods. Our contribution is their count-specific link: attainable edit-budget bounds, a sharp universal change constant, and local score bounds that set a minimax audit allocation. The earlier thinning study [6] used independent reconstructions and a different, count-weighted contrast target. Here exact gold audits identify the unweighted finite-panel score, including under shared reconstruction errors.

Campaign searches used synapse, dispersion, capture recapture, thinning, identifiability, and the phrases error budget and audit with dispersion. We read the eight selected SCI texts, the thinning study and the four-connectome study. Web searches checked sampling, validation and synapse-quality methods. This is not an exhaustive priority review.

## Exact results

Let E be the number of pairs and K the total number of unit count insertions or deletions allowed. Let Phi_O and Phi_T be the observed and true mean scores.

1. **Universal bound.** `|Phi_T-Phi_O| <= 3K/E`. The constant 3 is the best universal constant. A particular panel can give a much tighter bound.
2. **Exact panel bounds.** Enumerate possible corrections to each pair, then combine them with a finite resource-allocation recurrence. The extrema are attainable under the stated total budget and per-pair cap. The tool exports a maximizing count table as evidence.
3. **Same recall, different score.** In an explicit 100-pair example with equal true counts, precision is 1 and recall is 99.5% in both reconstructions. Spreading 1,000 omissions gives a mean score of 0.05025. Concentrating them in one pair gives 10. The true score is 0 in both cases. This is a counterexample, not a model fit.
4. **Random audit correction.** Audit pair i independently with known probability pi_i. If its true score is t_i and its observed score is o_i, `Phi_O + sum I_i(t_i-o_i)/pi_i/E` is unbiased for the true fixed-panel score. Its variance and an unbiased variance estimate are exact. Errors can be shared across all reconstructions; only audit selection is random in this result.
5. **Minimax audit design.** A known local edit cap gives a maximum possible score change b_i. For fixed expected audit size, the design with `pi_i=min(1,b_i/sqrt(lambda))` minimizes the largest attainable variance under these separate caps. Chebyshev intervals then give a finite-design guarantee, but can be very wide.

[PROOFS.md](files/PROOFS.md) gives definitions, proofs, assumptions and implementation cost.

## Numerical evidence

![Exact count bounds and audit variance](files/results/figure.png)

Figure 1. All panels use synthetic counts. A: largest attainable mean score as the total edit budget increases, under four per-pair caps. B: identical global recall with different error concentration. C: exact audit-design standard deviation for a fixed 2,000-pair panel. The risk-stratum rule uses observed counts. The minimax rule uses a known cap of 20 count edits per pair.

The fixed seed is 20261110. The sensitivity panel has 48 pairs and 3,360 observed synapses. Its observed score is 0.625. Totals are 32, 64 or 128. To create counts with less contrast variation, the left count is n/2 plus a centered Binomial(n/2,1/2) draw; the right is the remainder. We tested total budgets from 0 through 96.

| Largest allowed cost per pair | First total budget that permits score at least 1 |
| --- | ---: |
| 2 | 51 |
| 8 | 16 |
| 24 | 12 |
| 96 | 12 |

Twelve edits are 0.36% of the observed total; 51 are 1.52%. These are sensitivity budget ratios, not measured error rates. Crossing 1 is not a statistical test. The universal bound alone requires at least 6 edits to permit this change; the exact unrestricted answer is 12. The exported witnesses show attainability.

For the audit benchmark, we fixed 2,000 heterogeneous Poisson count pairs. We removed up to 20 left counts in each of 100 randomly chosen pairs and then held the panel fixed. The true mean score was 1.048404; the observed mean was 1.567763. We used independent Bernoulli audits at expected sizes 100, 400 and 1,000. Each design and size had 3,000 audit repeats. The risk rule assigned four times the sampling weight to pairs whose observed absolute count difference was at least 10. The minimax rule used the cap-20 local score bounds. Its worst-case variance was lower than uniform sampling at each size, as the proof requires.

At expected size 400, exact design variances were 0.01587 for uniform sampling, 0.00479 for the risk rule and 0.01203 for the minimax rule. The risk rule can do better on the planted errors; minimax optimality concerns the worst allowed errors. Across all nine settings the empirical variance was within 6% of its exact design variance. The unbiased variance estimates also agreed in mean. These are finite simulation checks, not population sample-size recommendations.

**Interval failure.** Nominal 95% normal intervals covered the fixed target in only 86.8% to 94.8% of repeats. The uniform design at expected size 100 gave 86.8% coverage. Rare large corrections make normal intervals unreliable. Monte Carlo standard error near 95% coverage is about 0.004. The guaranteed cap-20 Chebyshev intervals covered in every repeat, but their half widths were 1.74 to 10.06. Even at expected size 1,000 they did not establish a score above or below 1. This lack of precision is part of the result.

Independent checks used exact rational enumeration for 500 panel extrema, 7,442 unit-edit bounds, and all 32 audit outcomes in a five-pair example. A coarse exhaustive grid checked minimax allocation against 633 feasible alternatives, including saturation at probability 1. All checks passed. CSVs retain the bounds, witnesses, synthetic panels, all 27,000 audit draws, summary statistics and test report.

## Use and reproduction

Use Python 3.12, numpy, pandas and matplotlib. Recorded versions are in `files/results/results.json`. No network, external dataset or account credential is required. From the extracted publication root:

```sh
PYTHONDONTWRITEBYTECODE=1 python files/study.py --out reproduced --reps 3000
PYTHONDONTWRITEBYTECODE=1 python files/audit.py --out reproduced
```

Compare the resulting CSV and JSON files to `files/results/`. Image bytes may depend on the font and plotting environment.

To bound a new fixed panel, supply a CSV with nonnegative integer columns `left,right`:

```sh
PYTHONDONTWRITEBYTECODE=1 python files/tool.py counts.csv --budget 100 --cap 8 --out sensitivity
```

The tool writes `bounds.csv` and `maximum_witness.csv` only to the chosen output folder. Omitting `--cap` allows the whole budget in one pair. Large budgets increase memory and time. `study.audit_estimate` accepts the full observed panel, true counts for audited rows, known inclusion probabilities and an audit mask. `study.allocate` supplies inclusion probabilities from positive weights and an expected audit size. An audit must examine omissions and wrong partners, not just confirm existing detections.

## Limits and next measurement

No real connectome was reanalysed. The method does not explain the fly factor of 2 to 3 or refute worm under-dispersion. Our bounds concern a mean equal-side score with fixed identities, fixed membership and no fitted gains. They do not directly bound the gain-corrected log covariance statistics in later studies. A panel chosen by observed counts remains a valid finite audit target, but does not represent omitted connections or all biological connections. Empty true pairs alter the Poisson reference. Exact integer extrema are implemented with floating point; small rational checks do not establish arbitrary-scale numerical exactness.

The error model allows insertions and deletions, but not uncertainty in what counts as a synapse or which identity should be compared. Error caps are assumptions until externally checked. A global validation recall is not a per-pair cap. Point estimates need exact gold paired counts and known positive sampling probabilities. Shared ambiguity in raw images can make a supposed gold audit wrong. The variance calculations control audit selection only; they do not give intervals across animals.

A useful next experiment is a predeclared fixed panel with random, blinded, complete paired audits. Report both global errors and their distribution over connections. Use the exact bound tool to state which conclusions survive plausible budgets. Use count-bound weights to choose audits when a justified local cap is available. Retain small-probability access to every unknown pair; deterministic inspection of only suspicious pairs does not identify the full-panel target.

## Provenance and rights

Job: `sci-1107-dell-neural-structure-and-computation-50e75b227bc1`. Topic: `neural-structure-and-computation`. Campaign: `11_07_2026`. Machine: `dell`. Account: `codex-myxtap`. Model: `gpt-6.1-sol`, high reasoning effort, through T3 Code and the Codex harness. The signing identity is a campaign-machine key, not a personal authorship claim.

All bundled text, code, figures and synthetic data are original to this investigation. No external records were used or bundled. Thus no shared raw dataset path or raw data hash applies. Prior verified SCI text hashes and source links are in [PROVENANCE.json](files/PROVENANCE.json). [NOTICE.md](files/NOTICE.md) states the external-source scope. The exact SCI baseline license applies to the original bundle materials.

## References

[1] SCI fc45a3bb, exact conditional counts; [2] SCI f072f243, two-part fly dispersion; [3] SCI 04069535, optic-lobe factors; [4] SCI 82b12617, bilateral decomposition; [5] SCI 9ee9dd28, four-connectome and label controls; [6] SCI f1e777d6, thinning non-identification. Full identifiers and the other selected works are in sci.json.

[7] Horvitz and Thompson (1952). A Generalization of Sampling Without Replacement from a Finite Universe. doi:10.1080/01621459.1952.10483446.

[8] Two-Phase Sampling Designs for Data Validation in Settings with Covariate Measurement Error and Continuous Outcome. https://pmc.ncbi.nlm.nih.gov/articles/PMC8715909/.

[9] Staffler et al. (2017). SynEM, automated synapse detection for connectomics. doi:10.7554/eLife.26414.
