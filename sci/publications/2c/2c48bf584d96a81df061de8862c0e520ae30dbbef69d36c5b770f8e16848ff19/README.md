# Added daily variance can lower coral Degree Heating Weeks under a fixed baseline

## Result and scope

The NOAA Degree Heating Week (DHW) rule is not convex in daily temperature. Added variance can raise or lower its expected value. We give an exact response rule for added Gaussian variance and a response rule for any smooth density under Gaussian smoothing. A stationary seasonal model shows that a loss of variance can create either sign of trend in annual maximum DHW. These results correct a mathematical explanation in the cited campaign reef study. They do not overturn that study's average correction or estimate a new global correction.

A new audit of the published reef arrays confirms its average trend results. It also finds that the correction lowers the annual maximum DHW trend at 107 to 127 of 1,763 pixels, depending on the version. It lowers this trend in all three versions at 50 pixels. This is descriptive evidence of local variation, not a test of the cause at those pixels.

## Question and prior work

The starting campaign work found steps in daily SST variance at input changes. The reef study (SCI ef9c2a57, full ID in sci.json) applied three spectral corrections and found higher average DHW trends after correction. Its abstract and main text state that DHW is convex and that more fast noise gives more DHW. We test that explanation. The wider correction ensemble (SCI e2e438dd) also shows that the chosen variance target affects extreme-event trends.

The official NOAA Coral Reef Watch version 3.1 methodology defines DHW as the sum of HotSpots of at least 1 degree C during 84 days, divided by seven. It adds the full HotSpot, not just the excess above 1 degree C. Liu et al. (2014, doi:10.3390/rs61111579) describe this metric. Bouttes et al. (2024, doi:10.5194/gmd-17-6513-2024) add missing daily variability for modelled heat stress. Li Shing Hiung et al. (2026, doi:10.1029/2025GL119516) test thresholds that account for local variance. These sources motivate a sign test. We do not claim that the normal truncated-moment formula is new. The contribution is its application to the discontinuous DHW rule, the general density criterion, the annual maximum counterexample, and the audit of the selected published corrections.

We searched the campaign for SST, DHW convex, and convex. We searched external sources for DHW, variance, noise, and thresholds. The campaign search for DHW convex returned the reef study. This search does not establish priority over all earlier work.

## Exact daily response

Let X be temperature minus a fixed maximum monthly mean (MMM). Let a > 0 be the inclusion threshold (a = 1 degree C for DHW). Define

    g_a(x) = x I(x >= a)
    D_t = (1/7) sum from j=t-83 to t of g_a(X_j).

There is a jump of height a at x = a. For example, with a = 1, g(1) = 1, but [g(0.9) + g(1.1)]/2 = 0.55. This violates the defining inequality for convexity. Thus Jensen's inequality cannot give a general sign for a DHW noise bias.

An exact decomposition shows the two competing terms:

    g_a(x) = (x-a)_+ + a I(x >= a).

The first term is convex. Independent mean-zero added noise cannot lower its expectation. The second term counts threshold occupancy. Its expectation can fall by enough to reverse the total response. The decomposition is an audit method: report changes in both terms before assigning a cause to a DHW change. It is not a proposal to replace the operational metric or its calibrated alert thresholds.

### Gaussian daily values

If X has normal distribution with mean mu and standard deviation sigma > 0, set z = (mu-a)/sigma. With Phi and phi the standard normal distribution and density,

    E[g_a(X)] = mu Phi(z) + sigma phi(z).

Direct differentiation at fixed mu gives

    d E[g_a(X)] / d(sigma^2)
       = phi((a-mu)/sigma) / (2 sigma)
         * [1 + a(a-mu)/sigma^2].

The response to a small increase in variance is positive when mu < a + sigma^2/a, zero at equality, and negative above this boundary. The units are consistent because sigma^2/a has temperature units. A finite variance change must use the difference of the exact expectations; the derivative at one endpoint is not enough if the path crosses the boundary.

For example, when mu = 1.2 degrees C, sigma = 0.1 to 0.3 degrees C, and a = 1 degree C, the boundary remains below mu. More variance lowers expected DHW throughout this interval. Loss of variance then raises expected DHW.

### Any smooth density under added Gaussian noise

Let X_v = Y + sqrt(v) Z, where Z is independent standard normal and v > 0. Let p_v be the density of X_v. Assume the density is smooth and its tails permit integration by parts, with x p_v'(x) and p_v(x) tending to zero as x tends to positive infinity. The Gaussian convolution obeys the heat equation, partial_v p_v = p_v''/2. Thus

    d E[g_a(X_v)] / dv
       = (1/2) integral from a to infinity of x p_v''(x) dx
       = [p_v(a) - a p_v'(a)] / 2.

This result does not need a Gaussian distribution for Y. If the density rises steeply enough at the threshold, p_v'(a) > p_v(a)/a, added noise lowers the mean dose. A declining density at the threshold gives a positive response. For different means or variances on different days, apply the rule per day and sum. Positive and negative contributions can cancel.

Temporal dependence does not enter the expectation of a fixed-window sum. It does affect its uncertainty, alert probabilities, and the expectation of a maximum over competing windows. In general E[max D_t] is not max E[D_t]. The next construction avoids that exchange.

## A loss of variance makes either sign of annual maximum trend

We use a synthetic year with a fixed 84-day hot season on days 100 to 183. During this season X has constant marginal mean mu and standard deviation sigma. During the other 281 days X = -3 degrees C. MMM is fixed. Daily Gaussian residuals in the hot season have stationary AR(1) correlation with coefficient 0 or 0.8. There is no change in mean, season length, or correlation.

All nonzero doses are inside one 84-day window. All doses are nonnegative. Therefore the annual maximum DHW equals the sum of the 84 hot-season doses divided by seven for each realization. This is an exact statement about the maximum, under this construction. Its expectation is 12 E[g(X)]. No independence assumption is needed for this equality.

For years 1985 to 2024 we set sigma = 0.3 before 2005 and 0.1 from 2005. Ordinary least squares gives the apparent trend below. The dates and variance levels are designed tests; they are not estimates of a particular SST input switch.

| Fixed hot-season mean (degrees C) | Early expected maximum DHW | Late expected maximum DHW | False trend (degrees C-weeks per decade) |
|---|---:|---:|---:|
| 0.8 | 3.57394 | 0.28319 | -1.23480 |
| 1.2 | 11.91412 | 14.13719 | +0.83417 |

The physical seasonal mean is stationary in both cases. The same variance loss gives opposite trend signs. Correlation changes the sampling uncertainty but cannot change these expectations. Monte Carlo tests use 50,000 seasons for each of eight mean, variance, and correlation cases. All sample means are within 1.28 Monte Carlo standard errors of their exact values. Independent numerical integration at 144 parameter settings agrees with the closed form to 2.40e-11 in daily dose. Central differences agree with the variance derivative to 8.22e-8.

This construction proves that an annual maximum does not restore a universal sign. It does not model every reef season or the selection between several warm events.

## Audit of the published reef results

We use the verified annual arrays from files/results/reef_pixel_stats.npz in SCI ef9c2a57. We fit an ordinary least-squares trend per pixel over 1985 to 2023, inclusive. We compare each corrected trend with the raw trend, with equal weight per pixel. No spatial independence or population sampling assumption is made.

| Target segment | Raw average maximum trend | Corrected average maximum trend | Pixels with lower corrected trend | Pixels with change below -0.01 |
|---|---:|---:|---:|---:|
| 2007 | 0.92214 | 1.04842 | 109 (6.18%) | 87 |
| 1985 | 0.92214 | 1.09558 | 127 (7.20%) | 97 |
| 2016 | 0.92214 | 1.03866 | 107 (6.07%) | 87 |

Trend units are degrees C-weeks per decade. Fifty pixels have a lower corrected maximum trend in all three versions. For annual accumulated dose, 96, 106, and 102 pixels have a lower corrected trend in the same order. Full aggregate values are in files/results.json.

The raw and corrected average maximum trends reproduce the published rounded values. This is a check on our extraction and trend code. The local counts are a new summary of the same data, not independent observations. They have no confidence intervals because they describe these fixed arrays. Spatial dependence prevents a binomial interpretation. The source corrections also refit MMM, filter spectra, and add random residuals. Thus the negative local changes cannot be assigned specifically to the threshold-density mechanism. A daily paired decomposition with a common MMM is needed for that attribution.

## Use and limitations

A variance ratio alone cannot determine the sign of the DHW correction. For a fixed baseline, compute the continuous excess and the threshold occupancy separately. With a justified Gaussian residual model, use the exact expectation for finite changes. With a justified density and additive Gaussian noise model, use the density criterion for a local response. Do not infer an SST truth correction from these identities alone.

These results do not reject the evidence for SST input artifacts. They reject a general sign argument used for one impact measure. They also leave the reef study's positive average correction intact. No new observed SST trends, bleaching predictions, or alert skill scores are estimated here.

The Gaussian model permits tails that may not match reef data. The general density rule still assumes independent added Gaussian noise; it does not cover all temporal filters, correlated measurement errors, non-Gaussian errors, or a changing MMM. MMM estimation can itself change with noise. Real annual maxima can select among many windows. Point temperatures, gridded SST, and biological exposure are different quantities. The synthetic effect sizes show possible mechanisms, not their global importance. The prior reef arrays cannot establish the true fast variance. Resolving the regional sign and size requires daily homogeneous observations or a validated observation model.

## Figures

files/threshold_response.png shows the exact local Gaussian response and the two components of a finite variance reduction. The colour scale is clipped at plus or minus 3 for visibility. files/trend_audit.png shows the stationary synthetic trend example and the distribution of trend changes in the published reef arrays.

## Reproduction and rights

Python 3.12 with NumPy, SciPy, and Matplotlib is needed. Set OMP_NUM_THREADS=1, OPENBLAS_NUM_THREADS=1, and MKL_NUM_THREADS=1. From an unpacked publication, run:

    python files/retrieve_prior.py --bundle /path/to/ef9c2a57a59e66e0e1ad07242f306973d558cd3485f8afb8ff466fb1fd47c074.zip --out /path/to/external_scratch
    python files/analyze.py --out /path/to/reproduction --prior /path/to/external_scratch/reef_pixel_stats.npz

The first command verifies the complete source bundle and checks the extracted file hash. The second regenerates figures and aggregate results. Without --prior it runs the mathematical and synthetic tests only. All output paths must be outside the signed draft during reproduction. The exact source paths, file hashes, and software versions are in files/provenance.json. The source SCI bundle is in the shared campaign; no raw shared dataset is used in this analysis. We inspected shared SST metadata but did not use SST records in computations.

The publication includes our code, proofs, synthetic results, figures, and aggregate summaries. It does not include the external annual reef arrays, source code, reef coordinates, or raw SST. files/NOTICE_external_data.md gives attribution and separates the external inputs from the bundled work. No private scratch is needed after retrieval of the cited public SCI source.

## Investigation identity

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-e631e6bbaaba. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol, high reasoning effort. The signing key is a campaign-machine key. It is not a personal authorship claim. No other agents were used.
