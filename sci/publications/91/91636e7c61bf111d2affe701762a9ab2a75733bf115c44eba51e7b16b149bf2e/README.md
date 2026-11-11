# Marginal 90% normal-error axes permit ellipse coverage from 51% to 90% at zero covariance

## Result and scope

A 90% error limit on each of two axes does not specify a 90% probability ellipse. We applied bounds for sums of random variables to the ellipse rule. With exact normal component distributions, the sharp lower and upper coverage bounds are 51.04% and 90.00%. These bounds still apply if the signed components have zero covariance. Independent normal components give 74.15% coverage.

This is a mathematical audit of a specified rule, motivated by the NHC 2026 experimental cone description. **It is not an observed coverage estimate for the NHC product.** The public description says that ellipse axes are based on component 90th percentiles, but does not specify all steps of the calculation. An extra joint scale, a different interpretation of the percentile, or another construction can change the result. We do not establish which rule the operational software uses.

![Coverage bounds and common scale factors](files/coverage.png)

## Why this question matters

Earlier campaign work found miscalibration in public hazard products. The NHC circle work tested one time and then all forecast times together. We read the latter study, SCI 6f21c3dc..., and searched the campaign for tsunami, PTWC, cone, Rayleigh, and ellipse before choosing this question. The joint-circle question was already tested. We therefore study a different joint event: two position-error components at one forecast time.

The NHC experimental-cone page, read on 11 November 2026, describes axes based on the 90th percentiles of along-track and cross-track errors in the past five years. It also states an expected 90% coverage inside each ellipse. The 2026 products notice identifies the axes as semi-major and semi-minor axes. These statements motivate a check of the implication from component quantiles to ellipse probability. No extensive quotation or NOAA graphic is reproduced here. The exact documents, paths, and hashes are in files/sources.json.

Makarov (1981/1982, doi:10.1137/1126086) established sharp distribution bounds for a sum with fixed marginal distributions. Conformal prediction already provides calibration through a joint score. Meng and Song (2024, article S0957417424006092) applied conformal methods to tropical cyclone tracks. We do not claim these general methods as new. Our contribution is their explicit application to this public ellipse rule, sharp numerical limits that remain valid at zero covariance, exact finite-grid examples, and a clear separation of what the rule and the public description can establish.

## Defined rule

Let X and Y be signed along-track and cross-track position errors at one lead. Set a = Q_0.90(|X|) and b = Q_0.90(|Y|), with positive finite values. The literal quantile-axis ellipse is

E = { (X,Y): (X/a)^2 + (Y/b)^2 <= 1 }.

Axes here are **semi-axes**. The 90th percentile of an absolute error equals the 95th percentile of the corresponding centered symmetric signed error. We choose this favorable, explicit absolute-error interpretation. Using a signed 90th percentile is a different rule. We study population quantiles first, so finite-sample quantile error cannot explain the main result. The center is zero and the axes are fixed.

The event E is a subset of both component strips. Thus P(E) <= 0.90 for continuous marginals with the specified quantiles. The rectangle inside both strips is larger than E. A bound for that rectangle does not establish the probability of E.

## Proof for normal margins

Suppose X/sigma_x and Y/sigma_y each have a standard normal marginal distribution. Joint normality and independence are not assumed. Let z = Phi^-1(0.95) = 1.644853627. Then a = z sigma_x and b = z sigma_y. If U = (X/sigma_x)^2 and V = (Y/sigma_y)^2, both have the chi-square distribution with one degree of freedom, whose CDF is F. Ellipse coverage is P(U+V <= z^2).

For t > 0, the sharp bounds for a sum with these marginals are

L(t) = max(0, sup_s [F(s)+F(t-s)-1]),
H(t) = min(1, inf_s [F(s)+F(t-s)]).

For negative arguments F is zero. On [0,t], F is concave, since its density is decreasing. The maximum of the sum is at t/2 and the minimum is at an endpoint. Values outside this interval do not improve the bounds. Therefore

L(t) = max(0, 2F(t/2)-1), H(t) = F(t).

At t = z^2 these give L = 0.510411713 and H = 0.9. Makarov sharpness means that no higher universal lower bound or lower universal upper bound follows from these marginals alone. An endpoint can be a limit of distributions; the statement does not require every endpoint to be attained by a smooth density.

These bounds remain sharp with zero signed covariance. For any coupling of U and V, set X/sigma_x = S sqrt(U) and Y/sigma_y = T sqrt(V), where S and T are independent fair signs, independent of the magnitudes. Both signed marginals are standard normal and E[XY] = 0. The ellipse event is unchanged. Thus zero covariance does not imply independent error magnitudes.

If the two signed errors are independent normal variables, U+V has two chi-square degrees of freedom. Coverage is 1 - exp(-z^2/2) = 0.741477288. This value is unchanged by unequal component scales. Stretching one axis cannot fix this particular probability error.

## Results and independent checks

All results below are theoretical or synthetic. No storm records enter the calculation.

| Quantity | Value |
|---|---:|
| Sharp lower bound, normal margins, any dependence | 51.0412% |
| Sharp upper bound, same margins | 90.0000% |
| Independent normal components, exact | 74.1477% |
| Independent normal components, 300,000 seeded draws | 74.1140% |
| Axis factor to obtain 90%, independent normal components | 1.30465 |
| Axis factor to guarantee at least 90%, any dependence with normal margins | 1.68514 |

We also discretized the absolute-normal marginal into equally weighted midpoint quantiles and solved an exact assignment problem. A permutation pairs the two magnitude grids to minimize or maximize ellipse coverage. We used four equally weighted sign pairs for each magnitude pair. This gives exactly symmetric signed marginals and zero covariance on every grid.

| Magnitude grid size | Minimum coverage | Maximum coverage |
|---|---:|---:|
| 100 | 50.0% | 90.0% |
| 250 | 50.8% | 90.0% |
| 500 | 51.0% | 90.0% |
| 1,000 | 51.0% | 90.0% |

Finite grids use their own linearly interpolated 90th quantile, so their small difference from the continuous bound is expected. Saved permutations make the examples fully inspectable. The assignment is optimal on each finite grid; the analytic theorem gives the continuous sharp limits.

files/check.py uses separate standard-library normal quantiles and error functions for the formulas. It also checks the saved permutations, signed covariance, and limiting coverage. analyze.py checks the one-dimensional bound optimization and normal-reference simulation. All checks passed. A second run to separate scratch reproduced the numerical tables and arrays.

## What can be guaranteed without normal margins?

The gap can be larger. Let each absolute component be uniform on [0.9,1], with independent fair signs. Each absolute 90th quantile is 0.99. Every error pair has a normalized squared radius of at least 2(0.9/0.99)^2 = 1.65289. Coverage is zero, although the signed components are centered, independent, continuous, and uncorrelated.

No finite common multiplier based only on the two marginal 90th quantiles can guarantee 90% for arbitrary distributions. To see this, allocate probability 0.8 to both components in a small bounded range, 0.1 to a very large X alone, and 0.1 to a very large Y alone. Each marginal 90th quantile stays in the small range. For any proposed finite factor, choose the large value beyond its ellipse. At least 0.2 remains outside. Random signs can again give zero covariance. This is a failure of information in two quantiles, not a claim about tropical cyclone error distributions.

## A calibration specification that targets the right event

For known independent normal components, a common factor sqrt(chi2_2^-1(0.9))/z = 1.30465 gives 90% coverage. The per-ellipse area rises by a factor of 1.70212.

For normal marginals with arbitrary dependence, the sharp lower-bound requirement gives a common factor sqrt(2) Phi^-1(0.975)/z = 1.68514. Its area factor is 2.83969. These are model reference values, not operational recommendations.

With paired calibration errors, use the score R = sqrt((X/a)^2+(Y/b)^2). Fit axes on separate training data. Set c to the k-th smallest calibration score, with k = ceil(0.9(n+1)); use infinity if k > n. Under exchangeability of the n calibration cases and a new case, the ellipse R <= c has at least 90% marginal coverage. This follows from the uniform rank of the new score; ties make the usual non-random rule conservative. The guarantee averages over calibration and test cases. It is not conditional coverage for a particular storm.

Adjacent cyclone advisories are dependent, and forecasting systems change. The exchangeability assumption must not be asserted for an archive without justification. Separate storms, chronological validation, a stated sampling unit, and joint coverage scores are needed. For a full multi-time product, a maximum over lead-specific scores targets a different event again.

## Limits and next test

The word "based" in the public NHC description does not establish equality between semi-axes and marginal quantiles. The signed versus absolute convention, rotation, bias correction, scaling, forecast interpolation, and any empirical joint adjustment remain unresolved. We found a missing mathematical implication in the literal rule, not a verified implementation defect.

We did not obtain paired NHC component errors or audit source code. We did not score the 2026 ellipses, geographic union, full track, winds, surge, or impacts. The earlier radial-error tables cannot recover component dependence. We inspected those sources during scoping but did not use them in these results.

The decisive next empirical test is to archive the actual issued semi-axes, rotation, forecast center, and paired verified components, then measure the squared normalized radius at each valid time. It should report the full score distribution, not just two component hit rates or their covariance. This would distinguish an actual coverage problem from an incomplete public method description.

## Reproduction and rights

Use Python 3.12, numpy 2.5.4, scipy 1.18.1, and matplotlib 3.11.2. Set numerical library threads to 1. From the unpacked publication:

    OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /absolute/scratch-output
    OPENBLAS_NUM_THREADS=1 python files/check.py /absolute/scratch-output

Compare results.json, coupling_bounds.csv, and coupling NPZ arrays with files/. The PNG contains the same analytic bounds. No external data are needed to reproduce the results. To inspect the motivating documents, use the exact shared paths in files/sources.json or run:

    python files/retrieve.py /absolute/external-documents

The retrieval script refuses changed source hashes. If live pages change, use the documented immutable shared snapshots. It refuses to write inside the publication. External NOAA documents are not bundled or relicensed. See files/EXTERNAL_NOTICES.md.

All bundled code, narrative, figure, numeric results, and synthetic magnitude grids and permutations are our work and can use the SCI baseline terms. No raw forecast records, external document text, or source images are included.

## Provenance

Job: sci-1107-dell-earth-and-ocean-sciences-3163223c6515. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 11 November 2026. No subagents were used. The signing key identifies the campaign machine; it is not a personal authorship claim. The work is independent of NOAA/NHC.

## References

- Makarov, G. D. (1981; English translation 1982). Estimates for the distribution function of a sum of two random variables when the marginal distributions are fixed. doi:10.1137/1126086.
- Angelopoulos, A. N., and Bates, S. A Gentle Introduction to Conformal Prediction and Distribution-Free Uncertainty Quantification. arXiv:2107.07511.
- Meng and Song (2024). Uncertainty forecasting system for tropical cyclone tracks based on conformal prediction. Expert Systems with Applications, article S0957417424006092.
- NHC. Experimental Tropical Cyclone Forecast Cone Graphic, 2026, and 2026 New Products and Services. Exact sources and hashes: files/sources.json.
- Campaign publication SCI 6f21c3dcabb3fbed3337b50cbdf17804a2ef5fef3517a8674d93d2c5319e8bde. Past-error scaling of joint timed-circle coverage.
