# A smooth opaque screen fits the 2023 ASASSN-14ko X-ray ingress under tested flicker models

Job: sci-1107-dell-astronomy-29b802bf8505. Topic: astronomy. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. Analysis date: 2026-11-11. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Result

The resolved 2023 X-ray decline does not require an intrinsic loss of emission. A straight opaque edge that moves across a steady, circular Gaussian source fits the published 0.2-2 keV light curve. A uniform circular source also fits. The Gaussian crossing scale is about 0.60-0.62 observer days when the assumed flicker correlation time is 0-0.2 days. These are fitted values, not confidence limits. They measure source width divided by speed, not an absolute source size.

The shape comparison changes with the flicker model. With independent multiplicative flicker, the Gaussian edge has twice the log likelihood advantage 41.5 over a clipped exponential decline, at the same parameter count. At fixed correlation times of 0.05 and 0.2 days this value falls to 19.6 and 11.6. At 0.5-2 days the two fits are almost equal. No calibrated significance or mechanism probability is assigned to these differences. An intrinsic source can follow the same smooth curve as a screen.

This result adds a time-domain test to the spectral test in SCI 9c84683e. That study found a grey decline and excluded a uniform change of cold absorption. It also retained an opaque screen as an alternative. Our result supports that caution: the full ingress shape does not remove the screen alternative. It does not dispute the observed X-ray clock or the later change in period. It does limit the use of that clock as a direct time of inner-flow shutdown.

![Ingress fits](files/ingress.png)

The top panel shows the published 2-ks points and three fitted mean curves, with flicker correlation time fixed at 0.2 days. The lower panel shows residuals. The smooth curves are mean models; correlated flicker is also in the likelihood. The fits do not enforce the published normalised flux values.

## Question and prior work

Can the 2023 ingress distinguish intrinsic dimming from a moving opaque screen through its shape? The campaign search for ASASSN-14ko returned related publications at the time of selection. We read the XMM spectral study, SCI 9c84683e, and the resolved Chandra study, SCI dc60fe15. We checked the screen-duration result, SCI 1d967481. The latter excludes a screen confined near the star within its stated bounds; our model does not impose confinement near the star. Thus the models test different claims.

Huang et al. (2025, arXiv:2506.15039v1) discuss changes of the inner disc and corona. Risaliti et al. (2011, DOI 10.1111/j.1365-2966.2011.19055.x) study opaque X-ray eclipses as probes of the inner source. Eclipse mapping and the use of occultation shapes are established methods. Our contribution is their test on the published resolved ASASSN-14ko ingress, with an explicit sensitivity test for correlated flicker. We do not claim discovery of a new class of model.

## Input and selection

The only record-level input is the verified table `files/results/xmm/xmm_pn_timeseries_bins.csv` from SCI sha256:9c84683e6d15fa5bfbc84bc1295a57bfe066ad5f70394fe11952d494b02c90d9. Its SHA-256 is `8f205a78a435828e348f56af8ce32ceb37b22cf03df2a272f3750a5a230a480a`. The table contains rates from ESA XMM-Newton EPIC-pn PPS products. It uses five bands and 2-ks bins. We do not download or fit new event data. No shared raw dataset path is used. The exact local published source is `./campaign/9c84683e6d15fa5bfbc84bc1295a57bfe066ad5f70394fe11952d494b02c90d9.zip`.

We sum the 0.2-0.5, 0.5-1 and 1-2 keV rates and add their reported error variances. This avoids the bright hard companion. Fit range: MJD 60170-60175.3, with 57 bins in visits 0900410201 through 0900410601. A constant floor comes from MJD 60175.3-60207.5, as in the source study. Its weighted rate is 0.0463762 +/- 0.0004049 count/s. Its error is a statistical error under a constant-floor model, not a bound on systematic error. The mean floor in the last ingress visits is somewhat lower; the model permits a floor shift with a Gaussian penalty.

We select the whole final bright visit, the three decline visits and the first faint visit. This includes the transition endpoints omitted by a fit restricted to the central decline. We also test removal of the last faint visit. These choices were made after inspection of the published analysis. This is an exploratory comparison, not a blind test.

## Models and likelihood

The mean rate is f + A S(t), with fitted floor f and amplitude A. Times are observer days. All models have five fitted parameters: A, centre or onset c, crossing or decay scale w, f, and fractional flicker amplitude j.

* Exponential: S = exp[-max((t-c)/w,0)]. This has a bright plateau and one decay time. It represents only one possible intrinsic decline law.
* Gaussian edge: S = Phi[-(t-c)/w], where Phi is the standard normal cumulative distribution. It is the uncovered fraction of a circular two-dimensional Gaussian behind a straight edge at constant projected speed. Here w = sigma/v.
* Uniform circular source: S = [acos(z)-z sqrt(1-z^2)]/pi, with z = (t-c)/w clipped to [-1,1]. Here w = R/v.
* Logistic: S = 1/[1+exp((t-c)/w)]. This is a further smooth comparison curve and is not assigned a physical mechanism.

For residual vector r, minimise

`NLL = 0.5 [r^T K^-1 r + log det K + ((f-F)/Fe)^2]`,

where `K_ij = delta_ij e_i^2 + (j A)^2 S_i S_j exp(-abs(t_i-t_j)/tau)`.

At tau = 0 the flicker kernel is the identity. This is multiplicative Gaussian flicker, not Poisson noise or a full physical model of accretion. We fix tau successively to 0, 0.05, 0.2, 0.5, 1 and 2 days. The same covariance form and parameter bounds apply to every shape. Differential evolution uses a fixed seed and one process. It fits mean shape and flicker amplitude together. Bounds are in the source code. Rate units are count/s. Constants common to every fit are omitted, so NLL can be negative. We do not compare absolute NLL across different data subsets or bands.

The Gaussian and circular-source formulas follow by integrating the surface brightness on the uncovered side of the edge. `validate.py` checks both against separate numerical integrals. Maximum absolute error is 2.26e-14.

## Fit comparison and uncertainty

Twice the log likelihood advantage over the exponential (positive favours the listed shape):

| Fixed flicker time (d) | Gaussian edge | Circular source | Logistic |
|---|---:|---:|---:|
| 0 | 41.51 | 43.43 | 26.75 |
| 0.05 | 19.57 | 22.36 | 9.58 |
| 0.2 | 11.62 | 14.34 | 5.24 |
| 0.5 | 0.16 | 4.11 | 0.28 |
| 1 | -0.14 | 0.55 | 0.15 |
| 2 | -0.55 | -0.44 | 0.12 |

![Flicker sensitivity](files/comparison.png)

No likelihood ratio in this table is a p value. Shapes are not nested. Tau is not independently measured. For the Gaussian fits at tau = 0, 0.05 and 0.2 d, the residual quadratic forms r^T K^-1 r are 67.59, 66.83 and 66.48 for 57 bins. These are descriptive checks; fitted covariance parameters prevent a simple degrees-of-freedom interpretation. The best Gaussian scale at tau = 0.05 d is 0.6033 d, and its midpoint is MJD 60172.0625. At tau = 0.2 d the values are 0.6166 d and MJD 60171.9371. These midpoint times are model parameters; they are not replacements for the published deep-suppression times. At tau = 0.5-2 d the Gaussian scales span 0.65-1.22 d. The amplitude or flicker parameter can reach a bound at long correlation times. The circular-source amplitude reaches its upper bound from tau = 0.2 d onward. Such fits do not give precise source sizes.

Removing the last faint visit leaves 44 bins. At tau = 0.2 d, the Gaussian and circular-source advantages are 9.29 and 12.04. Fits to only the five visit means give advantages 9.74 and 12.11. Five means with five fitted parameters cannot support a calibrated shape test; this is only a check that the trend is not produced solely by the number of short bins. For four separate bands, Gaussian crossing scales at tau = 0.2 d are 0.647, 0.678, 0.700 and 0.564 d from soft to hard (through 4.5 keV). These values show no order-of-magnitude source-size separation. Without joint band covariance and confidence regions, they do not establish equal sizes or a size ratio bound.

We report the dependence on noise assumptions in place of a single error bar that would hide it. There are only five visits through the transition and gaps of about one day between them. We do not claim that the screen is detected, that the exponential is physically excluded, or that Gaussian and circular brightness profiles can be separated.

## What a screen would require

For any differentiable, monotonically decreasing fraction S(t), a straight edge at speed v admits the nonnegative projected brightness

`g(x) = -S'(x/v)/v`.

Its integral is one when S falls from one to zero. A nonnegative separable surface brightness `I(x,y) = g(x) h(y)`, with integral h = 1, gives that same light curve. Thus even a perfect single-band decline cannot by itself identify dimming versus occultation without restrictions on the source and screen. Equal fractional curves in several bands require proportional projected brightness profiles over the scanned region. They do not require the same two-dimensional source. The simple circular examples above show that the observed decline need not require an irregular source. Relativistic transfer, source inclination and a curved edge are outside this construction.

The long faint interval gives a useful conditional geometry test. Consider an opaque strip of length L in its direction of motion that covers a Gaussian source. To keep the uncovered fraction below 0.05 for a continuous interval T, each edge must be at least 1.64485 sigma from the source centre at the relevant end of the interval. A necessary condition is

`L/sigma >= T/w + 3.2897`.

This follows because the interval of allowed centre positions inside the strip has length at most L - 2(1.64485 sigma). Integrating over both Gaussian tails can only strengthen the requirement. This bound assumes a steady source, a rigid strip, constant speed and a straight parallel leading and trailing edge.

Using T = 32 observer days, the lower span reported in SCI 9c84683e, and the fitted w = 0.6033 d at tau = 0.05 d, gives L/sigma >= 56.3, or about 23.9 source full widths at half maximum. At w = 1.2233 d the same calculation gives 29.4 sigma, or 12.5 full widths. These are conditional values, not confidence bounds. The finite sampling does not prove uninterrupted occultation for 32 days, and the data do not bound L without a bound on w. This points to an extended detached structure, rather than a compact cloud tied closely to the surviving star. It does not prove that such a structure can remain opaque, maintain a straight edge, recur, or survive shear.

## Scope and limits

This is a reanalysis of published pipeline rates. It does not provide a new independent instrument clock, a new spectral fit, or a mechanism for the stopped period change. The constant floor, rate errors, bin exposures and selection are inherited from the source study. We evaluate the curve at bin centres; bin averaging is negligible relative to a 0.6-day crossing scale for 2-ks bins. Background fluctuations, calibration error, pile-up, energy redistribution, and nonstationary flicker are not reprocessed. The reported floor uncertainty ignores serial floor variability. A Gaussian process permits negative flux perturbations and is only a statistical description. A joint fit of all bands would be needed for physical size-ratio limits.

The evidence against a uniform cold absorber remains. An opaque screen and an intrinsic drop both remain compatible with the grey change. The periodic event can mark geometry as well as a radiative transition. This is why the stopped timing curvature cannot yet be assigned to an inner-flow clock from the 2023 decline alone.

## Reproduction and rights

With Python 3.12, numpy, scipy, pandas and matplotlib, run:

```
python files/validate.py
python files/reproduce.py /path/to/campaign /path/to/separate-scratch
```

The retrieval script verifies the parent ZIP, extracts the exact table with `sci read`, checks its hash, and writes all regenerated output outside this publication. `analyze.py INPUT_CSV OUTPUT_DIRECTORY` runs the fits directly. A run takes several minutes on one CPU. No raw telescope download is required. Compare the generated `results.json` with the supplied aggregate results; small optimiser differences are possible. Files contain source code, fit summaries and two figures. Input records are not bundled. No private scratch is needed if the cited SCI bundle is preserved.

See `files/NOTICE_external_data.md` for attribution and external terms. The exact SCI baseline license applies to our code, text, figures and aggregate results. It does not relicense ESA source products. No remote upload or submission was made by this worker.
