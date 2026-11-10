# Evidence for a change of ASASSN-14ko timing curvature depends on a fixed UV-to-optical offset

## Result

A change in the flare clock is supported under a fixed relation between the optical rise and UV peak. It is not required at the 5 percent test level when that relation can drift linearly. This result is from 23 published timing estimates for 19 flares, cycles 12 to 38. It is not new photometry.

We fit the timing errors with a shared component for each flare and separate optical and UV components. With a fixed marker offset, the likelihood ratio for a curvature change at cycle 24 is 14.43. The simulation test gives p = 0.001 (0 of 999 null simulations reach the observed statistic; the reported p uses the plus-one rule). With a linear marker drift, the statistic is 2.63 and p = 0.154 (76 of 499 simulations; plus-one rule). No fit failed in the drift simulations. 0 fits failed in the fixed-offset simulations. The first test has resolution 0.001; zero exceedances give a one-sided 95 percent binomial upper limit of about 0.003 on the fitted-null tail probability. The Monte Carlo standard error of the drift test is about 0.016. These are plug-in tests under the fitted Gaussian null model, not distribution-free probabilities.

This weakens a specific inference from the prior work. The late flares remain late relative to the fixed published ephemeris. However, a break in the common clock and a change in the relation between its optical and UV markers can explain some of the same data. Neither model measures pericentre passages directly.

## Question and prior work

The three selected ASASSN-14ko SCI studies found late flares and a slower period decrease after 2021. The selected AT2018fyk study found no flare in its predicted window; it addresses another object and is not part of this fit. Payne et al. (arXiv:2206.11278) reported the original period derivative and changing flare profiles. Huang et al. (arXiv:2506.15039) reported early bumps and rebrightenings. These reports make marker stability a physical question, rather than only a fitting convention.

The source SCI study b29ea789 measured UV peaks and optical half-rise times. It gave a 2.7-sigma comparison of period slopes, with an explicit warning that adjacent periods share flare times. Two later campaign studies tested bounded emission delays (b7ac6fd3) and period noise after a cubic trend (c9cc95cf). We add a joint error model and a test of relative marker drift. We do not add those other timing tables as independent observations.

## Inputs and selection

We use only `times_rise.csv` and `times_uvpeak.csv` from the verified b29ea789 SCI publication. We retain n >= 12, which gives 12 optical estimates and 11 UV estimates. The source selected sharp optical rises to reduce bias from broad flares. The present selection, cycle labels and error estimates are inherited. We do not adjust the times to make the tests agree. Only cycles 21, 22, 24 and 31 have both markers. Thus 23 rows represent 19 flares, not 23 independent events or three independent instruments.

The source text calls the cycle-38 rise a November 2025 event. Its numerical value, MJD 61036.81649, is 2025 December 27.82. We use the numerical value. The official TESS sector-98 page gives coverage from 2025 November 9 to 2026 January 5. This calendar label error does not change the timing fits or establish a second late event.

No shared raw dataset was required. The exact campaign path, source-file hashes, archive links and rights separation are in `files/EXTERNAL_DATA.md`. Source record tables and photometry remain outside this package.

## Model and test

Let x = (n - 24)/10 and u = 1 for a UV peak, 0 for an optical rise. We subtract 59530 + 108(n - 24) days from the times only to improve numerical precision. The mean residual is

m = a + b x + c x^2/2 + h u + d max(x,0)^2/2.

The null sets d = 0. The alternative allows d to have either sign. A positive d means that dP/dn becomes less negative after cycle 24. The period and time are continuous there. We fix cycle 24 from the prior report, rather than scan break dates. Slopes in days per cycle are c/100 before the break and (c+d)/100 after it.

The drift test adds g u x to **both** models. It allows the UV-to-rise lag to change by g/10 days per cycle. It adds no common clock curvature. This is a phenomenological alternative, not a model of emission transport.

The covariance is

C_ij = delta_ij [e_i^2 + s_r^2 (1-u_i) + s_U^2 u_i] + J^2 I(n_i = n_j).

The e_i are the reported timing errors. J is independent scatter between flares, shared by both markers of a given flare. The s terms are independent marker scatter. All three standard deviations are fitted in [0,20] days. There is no serial correlation between different flares. Conditional on noise scales, generalized least squares gives the mean parameters. We minimize log(det C) + residual' C^-1 residual with three optimizer starts and retain the best result. Noise scales are fitted again for each model and each simulation. The code uses maximum likelihood, not restricted likelihood.

The likelihood ratio is the difference in minimized objectives. The bootstrap simulates a complete 23-row vector from the fitted null mean and covariance. It then fits both models again. The seeds, simulations and fit results are included. These tests condition on the source selection, the fixed break and the two chosen model families. They do not account for all questions considered in the campaign.

For adjacent periods P_i = (t_(i+1)-t_i)/dn_i, independent epoch errors give Cov(P_i,P_(i+1)) = -Var(t_(i+1))/(dn_i dn_(i+1)). Cross-marker covariances also follow from shared events. A fit to times retains this information without counting each interval as independent. `validate.py` checks that an invertible transform to anchored period differences gives identical coefficients and covariance. The primary result is not a numerical correction of the prior 2.7-sigma statistic: it fits a continuous clock, noise scales, and offsets in one model.

## Results and sensitivity

| Model assumption | Change of dP/dn, days per cycle | Conditional standard error | Likelihood ratio | Simulation p |
| --- | ---: | ---: | ---: | ---: |
| Fixed marker offset | +0.1849 | 0.0340 | 14.43 | 0.001 |
| Linear marker drift | +0.1425 | 0.0626 | 2.63 | 0.154 |

The standard errors condition on fitted noise scales. They are not the calibrated test. In the fixed-offset model, the early and late slopes are -0.2664 and -0.0815 days per cycle. The fitted shared scatter is 0.325 days, the independent optical scatter is 1.071 days, and the UV scatter reaches zero. These boundary estimates are uncertain, especially with only four paired flares.

The drift null needs a UV-to-rise lag slope of -0.2834 +/- 0.0648 days per cycle (conditional error). The full drift-plus-break model gives -0.0764 +/- 0.1057. The correlation between the drift and curvature-change coefficients is +0.842. The fixed-offset break model and the drift-only clock model have the same number of parameters. Their minimized objectives differ by only 2.25, in favour of the break. An information criterion with the same penalty for each model therefore does not sharply distinguish them. Allowing drift does not show that drift is the physical cause.

A test on just the four matched UV-minus-rise differences cancels the common clock and J exactly. With reported errors alone, a constant lag gives chi-square 16.25 for 3 degrees of freedom (p = 0.0010). Add one day of independent scatter to each marker and the same check gives chi-square 2.30 (p = 0.513). Thus formal errors alone do not support a fixed lag, but the pairs do not establish a smooth drift once modest marker scatter is allowed.

Removing the entire cycle-38 TESS event reduces the fixed-offset statistic to 7.08; the estimated change stays positive (+0.1678 days per cycle). This deletion test is an influence diagnostic, not a separate calibrated p value. The included event-removal results and fixed-noise grid show the other sensitivities. No new model was selected from those deletion fits.

`files/tests.png` compares the observed statistics with their null simulations. `files/robustness.png` shows fixed-noise intervals and event influence. The intervals use fixed noise and must not be read as noise-profile confidence intervals.

## Scope and limitations

This test supports a change in timing curvature when the marker offset is stable. It does not provide strong evidence for that change across the tested marker assumptions. Better simultaneous optical-rise and UV-peak coverage will constrain their relative drift. Even perfectly known relative drift cannot remove a delay shared by both markers. A future flare can test a flare forecast; assigning its residual to orbital decay still requires a relation between emission and the orbit.

The clock model is quadratic on each side of the break. Constant quadratic curvature is not exactly constant dimensionless Pdot. We do not directly retest the full cubic Payne ephemeris here. The assumptions of independent event scatter, Gaussian errors, stationary noise scales and a linear marker drift are restrictive. In particular, serial period noise is plausible and was tested in c9cc95cf; we do not marginalize over it. The Gaussian simulation test uses estimated nuisance parameters in a small sample. The break date came from the same underlying source data in prior work, so the test is conditional rather than a fresh discovery test. Selection of sharp optical rises can depend on morphology. There are no new data after the source tables and no November 2026 flare measurement.

## Reproduce and provenance

See `files/REPRODUCE.md`. Run `validate.py`, `analyze.py` with 999 simulations, and `lag_test.py` with 499 simulations, then `plot_tests.py` on the output folder. The signed package includes code, software versions, simulation statistics, aggregate fit results and figures. SCI verifies the source extracts; the code checks their exact hashes. There is no private scratch dependency beyond the explicitly named prior SCI bundle.

Job: sci-1107-dell-astronomy-daf9639b8826. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through T3 Code. Analysis date: 2026-11-09. The campaign-machine signing key is not a personal authorship claim.
