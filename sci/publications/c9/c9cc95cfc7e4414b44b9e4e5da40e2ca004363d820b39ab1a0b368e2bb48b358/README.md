# Finite sample tests support period noise beyond a cubic trend in the 2014-2026 ASASSN-14ko peak times

Job sci-1107-dell-astronomy-8fc86acc9791. Topic astronomy. Campaign 11_07_2026. Machine dell. Account codex-myxtap. Model gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. Analysis date 2026-11-09. The campaign-machine signing key does not establish personal authorship.

## Result

Random period changes remain supported in a restricted-likelihood test after a cubic timing trend is removed. Thus a smooth cubic change alone does not account for the correlation that this test detects in the selected peak times. A forecast made from the early peaks also favors the period-noise model over the cubic model. This extends the prior SCI work, which used a constant period drift and a large-sample boundary test for the noise claim. It does not add independent observations.

The inference has an important limit. Full profile maximum likelihood gives zero period-noise amplitude for both peak definitions, while restricted likelihood gives a positive amplitude. These are different procedures for the unknown mean. The data do not give an estimator-independent measurement of period noise. In particular, none of these tests shows that the orbit receives random kicks.

![Evidence and finite sample calibration](files/evidence.png)

## Prior work and question

Payne et al. (2021, 2023; arXiv:2009.03321 and 2206.11278) measured the changing flare recurrence time. SCI 9817499f... measured later peaks and proposed random period kicks. Its full-record test used half of a one-degree chi-square tail for a variance component on the boundary. It also noted that smooth higher-order evolution could compete. SCI b29ea789... used rise and UV markers and found a slower decrease after 2021. SCI b7ac6fd3... showed that bounded changes of emission delay can still permit constant orbital decay. We do not repeat that delay test.

Crainiceanu and Ruppert (2004), DOI 10.1111/j.1467-9868.2004.00438.x, explain why the usual boundary mixture can fail for a single correlated record. We apply a simulation calibration to this particular timing design. Huang et al. (2025), arXiv:2506.15039v1, report changes of flare structure that can affect the timing errors. The present test asks if a cubic mean can remove the period-noise evidence, under stated Gaussian noise assumptions. A cubic is a local description of a smooth change, not a complete physical alternative.

## Inputs and data boundary

The input is the verified SCI bundle 9817499f83bd750e5d908eefaa455212feb0ee7b9b0e7a3c620784dd93ba55b5. Each version contains the same 21 published peaks at cycles 0-24 and nine later peaks at cycles 25-38. The later peaks use either a template fit or a kernel maximum. The versions share the same observations and are sensitivity analyses, not two independent tests. The two published error sides are averaged. Times, errors, jitter and kick scales are in observer-frame days.

The source combines ASAS-SN aperture photometry and one TESS peak. No raw photometry is downloaded or measured here. The exact shared source path is /mnt/dell-data/campaigns/11_07_2026/9817499f83bd750e5d908eefaa455212feb0ee7b9b0e7a3c620784dd93ba55b5.zip. Internal paths, byte counts and SHA-256 values for each used table are in files/provenance.json. No file in the shared datasets store is used. Source tables remain in the source bundle and are not copied here. The new bundle contains code, aggregate results, fitted coefficients, synthetic test statistics and original figures. External-data rights are described in files/EXTERNAL_NOTICE.txt.

## Models and method

For integer cycle n, let the timing mean be a quadratic (Q) or cubic (C) polynomial. The quadratic corresponds to constant period change per cycle. It approximates the published small-derivative ephemeris; it is not an exact fit of the physical constant-Pdot model. The cubic allows a smooth change of period drift. Legendre basis functions on (n-19)/19 improve numerical stability. A fixed 56852 + 110n is subtracted before fitting and has no effect on these tests.

The covariance is

    V = diag(e_i^2 + s^2) + q^2 A A^T
    A_ik = max(n_i - 1 - k, 0), k = 0,...,max(n)-1.

Here e_i is the reported timing error, s is independent white timing scatter, and q is the standard deviation of an independent period kick at each integer orbit. This follows t_(n+1)=t_n+P_n and P_(n+1)=P_n+d+w_n. Kicks before the first observed orbit can be absorbed by epoch and period. R adds kicks to Q; CR adds kicks to C. Both include s. The same covariance is used for all models and forecasts.

For each fixed q and s, generalized least squares removes the polynomial coefficients. Full maximum likelihood profiles these coefficients. Restricted likelihood instead uses the exact Gaussian density of U^T t, where columns of U form an orthonormal complement to the mean design X. The implementation evaluates the equivalent determinant formula. An independent null-space calculation agrees to less than 3e-12 in negative log likelihood. Adding any quadratic mean leaves the quadratic restricted likelihood unchanged.

We optimize s in [0,15] and q in [0,5] days, with explicit q=0 and s=0 candidates and two starts for the two-parameter optimizer. The observed optima are far from the upper bounds. An independent 41 by 41 grid over s in [0,6] and q in [0,2] confirms the neighborhood of all observed optima. The two nested statistics are twice the restricted log likelihood gain for R over Q and CR over C. Restricted likelihoods with different mean spaces are never compared.

For each peak definition and each null mean, we simulate 999 records at the observed cycles and errors, with the null fitted white scatter and polynomial mean. Every simulated record is refitted under all four models. Seed: 20261109. The calibration retains gaps and error variation. The reported probability is (1 + number of simulated statistics at least as large as observed)/1000. It is conditional on fitted nuisance parameters and the Gaussian model, not an exact nuisance-free test. The reported Monte Carlo error is one binomial standard error. No probability below 0.001 can be resolved. These are exploratory tests without a correction for the choice of model family.

## Finite sample results

| Peak definition | Removed mean | q, days/orbit | Restricted LR | Null exceedances | Simulation p and MC error |
| --- | --- | ---: | ---: | ---: | ---: |
| template | Quadratic mean | 0.749 | 6.919 | 2/999 | 0.003 +/- 0.002 |
| template | Cubic mean | 0.971 | 5.625 | 4/999 | 0.005 +/- 0.002 |
| kernel | Quadratic mean | 0.624 | 9.904 | 1/999 | 0.002 +/- 0.001 |
| kernel | Cubic mean | 0.719 | 9.082 | 0/999 | 0.001 +/- 0.001 |

![Restricted tests and held-out scores](files/noise_forecast.png)

The fitted q values after a cubic mean are larger, not smaller, than after a quadratic mean. This does not mean that cubic evolution creates physical noise. Removing a mean mode changes both the residual space and the covariance estimate. The calibrated tests give evidence against independent white residual timing errors for these two smooth mean families.

A separate check simulates the fitted cubic model but scores the quadratic-versus-kick statistic. The observed statistic is exceeded in 95 of 999 template simulations and 29 of 999 kernel simulations (calibrated tails 0.096 and 0.030). Thus the quadratic noise test alone has limited ability to separate smooth curvature from period noise. The cubic-residual test is the more direct test of that distinction.

Full profile likelihood gives q=0 for Q and C in both versions. Its small-sample corrected information criterion, AICc, favors C over Q by only 1.85 (template) and 1.46 (kernel). R then adds an unused variance parameter. This is a warning about the treatment of estimated trends in a short correlated record, not a reason to interpret profile estimates as a proof of no noise. We report both procedures to show the inference limit. files/model_summary.csv contains only full-likelihood AICc values. No AICc is assigned to restricted fits with different mean spaces.

With the quadratic mean removed, the largest eigenvalue of the white-noise-whitened kick covariance supplies 63-64 percent of its trace. Its participation rank, (sum eigenvalues)^2 / sum squared eigenvalues, is 2.13-2.17. After a cubic mean this rank is about 2.49. These are covariance concentration measures, not counts of statistically independent observations or formal degrees of freedom. They show why a large-record boundary formula requires care here. The spectrum is in files/noise_modes.json.

## Forecast comparison

We fit all hyperparameters only to cycles 0-24. We then score the nine later peaks jointly without updates. Universal Gaussian prediction includes uncertainty in fitted polynomial coefficients and the full cross-cycle kick covariance. Hyperparameter uncertainty is not integrated. Higher log score is better.

| Peak definition | Q | C | R | CR |
| --- | ---: | ---: | ---: | ---: |
| template | -49.29 | -53.61 | -39.24 | -39.95 |
| kernel | -31.31 | -35.52 | -26.66 | -27.64 |

R improves on C by 14.36 log units for template peaks and 8.86 for kernel peaks. Allowing a cubic mean in the kick model gives a slightly worse score than R. This strengthens the specific case for a noise forecast over an extrapolated cubic forecast. It does not exclude other smooth models, such as a saturating period trend. The cubic extrapolation has large parameter uncertainty and misses the last peak by about 70 days. This forecast check uses already published held-out data and is not a new prospective observation.

The R forecast still has a large Mahalanobis statistic for template peaks (42.3 for nine times); for kernel peaks it is 15.2. Thus improved scores do not make R an adequate model for every peak definition. Structured broad flares can violate the independent Gaussian error assumption.

## Sensitivity and limits

Removing the TESS point leaves restricted Q-versus-R LR values 5.45 and 8.70 for template and kernel peaks. Removing the broad cycles 25 and 27 gives 5.30 and 2.87. The early record alone gives LR 6.27. These subset statistics have not been assigned bootstrap probabilities here; a full-record calibration must not be used for them. The input definitions and all subset fits are in files/results.json.

No new light curve or pericentre marker is obtained. We do not combine the three prior studies as independent data. Source peak errors, changing flare shapes, band changes, common calibration errors, and slow changes of emission delay can all affect the result. The input errors are treated as known. The null bootstrap uses a fitted jitter and assumes independent Gaussian white errors. Tests under other error distributions can differ. Noise strength and smooth drift share a small number of broad modes. We do not infer an orbital energy change, a stellar mass loss rate, or the absence of steady orbital decay. The analysis concerns the selected flare clock.

Under the tested error model, adding this cubic trend does not remove the restricted-likelihood noise evidence. It does not show that random kicks are the unique cause. Future independent timing markers and a longer record are needed to separate orbital noise from emission-delay changes. No new November 2026 flare is claimed or forecast here.

## Reproduce

Use Python 3.12 with numpy, scipy, pandas and matplotlib. Exact versions are in files/environment.json. Obtain the cited source SCI bundle in a campaign folder. Run from any directory, using separate scratch output:

    OPENBLAS_NUM_THREADS=1 python files/analyze.py --campaign /path/to/campaign --out /path/to/scratch --bootstrap 999
    OPENBLAS_NUM_THREADS=1 python files/forecast.py --campaign /path/to/campaign --out /path/to/scratch
    OPENBLAS_NUM_THREADS=1 python files/diagnostics.py --campaign /path/to/campaign --out /path/to/scratch
    OPENBLAS_NUM_THREADS=1 python files/plot_results.py --out /path/to/scratch

The source bundle is verified with sci verify. Input byte hashes are checked against its signed manifest before analysis. The scripts read records in memory and write only new aggregate or synthetic outputs. Do not write to the signed publication. Compare results.json, forecast_validation.json and noise_modes.json. Small optimizer and library differences can affect fitted coefficients near a zero boundary and Monte Carlo ranks. The mathematical contrast check must pass at 1e-7. The main tests should agree within Monte Carlo error if the simulation count or seed changes.

## Attribution

Peak times and their extraction method: SCI 9817499f... (job sci-1107-dell-astronomy-8d115448d674), with Payne et al., ASAS-SN and TESS as upstream sources. Other relevant SCI work: 9398601f..., b29ea789..., and b7ac6fd3.... Statistical method context: Crainiceanu and Ruppert (2004). Flare-shape context: Huang et al. (2025). All code in this publication is new campaign work; the prior analysis code was read for method comparison but is not copied.
