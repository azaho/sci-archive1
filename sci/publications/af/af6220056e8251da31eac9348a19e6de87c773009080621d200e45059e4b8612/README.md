# A two-day UV-driven echo does not fit the 2020 ASASSN-14ko optical flare under a fixed UV template

Job: sci-1107-dell-astronomy-b4d00cce774d. Topic: astronomy. Campaign: 11_07_2026.
Machine: dell. Account: codex-olen. Model: gpt-6.1-sol with high reasoning effort, Codex harness in T3 Code. Analysis date: 2026-11-11. The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

The short UV-to-optical rise lag does not describe the full response of the optical flare. We test cycle 20, the well sampled 2020 August-September flare of ASASSN-14ko. We use the new LCO nuclear flux measurements and the fitted Swift UVW2 profile in SCI e6845f16. A constant host plus **any nonnegative response on a 0-2 day grid** gives chi-square 56.12, 73.33 and 94.58 in g, r and i. A response on 0-24 days gives 8.99, 11.34 and 15.81. These are fits to 23, 25 and 24 optical measurements. The UV template and optical noise scales are fixed in these tests.

With twice the published optical white scatter, the fit gains remain 14.39, 19.44 and 33.23. Conditional null simulations give tail fractions of 0.0020, 0.0010 and 0.0005. These are plug-in simulation tests, not confidence limits that include UV model error or time-correlated calibration error. The three bands are not independent replications.

This result constrains the emission chain, not the orbit. If the measured UV profile is the input, the optical flare needs a longer response, a changing spectrum, a separate power source, or another change from the tested linear model. A near one-day rise lag alone cannot establish a response confined to that time scale. We do not measure a unique response function or a source radius. We do not prove that orbital decay stopped.

![Positive response fits](files/echo_support.png)

Figure 1. Top: LCO nuclear measurements, with errors that include the published per-band white scatter. Curves give the best positive response for maximum delays of 2 and 24 days; each fit has its own constant host. Bottom: minimum chi-square against allowed response support. The longer response has many free weights and can fit small features. Its good fit is not a detection of those features or of a specific transfer function. All times are in the observer frame.

## Question and prior work

The selected campaign work found a nearly constant X-ray recurrence in 2020-2024 and late flares relative to a constant period-derivative clock. Later work showed that this conclusion depends on the timing marker. SCI e6845f16 resolved early and late components in off-state flares. It also measured wavelength-ordered rise times in the on-state cycle 20. Relative to UVW2, the g and i half-rises are later by about 0.61 and 0.89 day. Its fitted UVW2 decay time is 13.24 days (posterior median); the optical values are 20.08, 25.72 and 31.82 days in g, r and i. This leads to a direct test: can a short echo explain the slow optical decline as well as the short rise lag?

The result is not a first report of wavelength-dependent flare evolution. Payne et al. (2021, arXiv:2104.06414) studied the 2020 flares. Huang et al. (2023, arXiv:2310.03236) reported bumps and rebrightenings. Huang et al. (2025, arXiv:2506.15039) studied changes in thermal temperature and radius. SCI da733a71 tested thermal heating for a 2023 X-ray-to-UV threshold delay. SCI b63437f8 tested extra passive delay between broad UV flare templates. Our test instead uses the full, resolved 2020 LCO optical profiles as outputs and the UVW2 flare as input, with no prescribed positive response shape. A campaign search for ASASSN preceded this choice and returned these related results. The search does not establish priority outside the campaign.

## Inputs and rights

No new archive images were downloaded. The only data source used in the calculation is the verified SCI baseline bundle e6845f1621bbd9268d3dddef62c52cb53863d1f5fb7085ff7da87120db353b7e. Its derived nuclear flux table and flare-fit table are under its SCI baseline terms. The code reads two files: `files/results/lco_phot_cal.csv` and `files/results/fits/fits_c19_20_29.json`. Exact hashes and the canonical shared campaign path are in `files/provenance.json`. No files from the shared dataset store were used. The original image frame IDs and reduction provenance remain available in the cited, signed source bundle.

The input tables stay in separate local scratch. This package contains our code, text, aggregate fit results and figure. It contains no image pixels, Gaia records or external database extract. See `files/NOTICE.md` for credit and terms.

## Method

We fit

`F_band(t) = B_band + sum_j h_j U(t - delay_j), h_j >= 0`,

where B is a free constant host level. U has unit peak, a half-Gaussian rise and an exponential decline. Its maximum-likelihood parameters from the source are peak MJD 59093.400865, rise sigma 1.557957 days and decay time 13.126696 days. The source amplitude is absorbed in h; no absolute UV-to-optical flux calibration is needed. The maximum delay D is tested at 0, 1, 2, 4, 8, 12, 16 and 24 days, with weights on a 0.5-day grid. This contains arbitrary mixtures of prompt and delayed emission on that grid. There is no smoothness penalty.

We apply the source quality cuts: status ok, convolution flag 1, zero bad nucleus pixels, finite flux, at least two ensemble stars, and zero-point frame scatter below 0.05. The time window is MJD 59088.118 minus 25 to plus 45 days. All selected frames are in the same instrument family. The variance is the squared reported error plus the squared source posterior-median white scatter. The scatter values are 29.91, 38.23 and 28.96 microJy in g, r and i (use the code and source for full precision). Weighted projection removes the constant host exactly. Nonnegative least squares then gives the global least-squares minimum for the response weights. We do not fit the response mean or its total delayed fraction, since the weights are not unique with these samples.

For the conditional simulation test, we draw Gaussian errors about the best D=2 prediction, with the stated fixed variances. Each of 1,999 draws is refitted at D=2 and D=24. The statistic is chi-square(2) minus chi-square(24). Tail fractions use `(1 + exceedances)/2000`. The seed is 11072026. This procedure accounts for the many response weights and their positivity boundary at this fitted null. It does not give a uniform test over every possible null response, and it does not propagate all upstream fit uncertainty. No nominal degrees of freedom or chi-square reference distribution is assigned to the long response fit.

A useful exact check explains the decline test. For t later than the UV peak plus D, every input term is on its exponential tail. Thus

`F(t)-B = exp[-(t-t_peak)/tau_UV] * sum_j h_j exp(delay_j/tau_UV)`.

Every finite short response must then have the same late decay time as the input. Response shape can change its amplitude but cannot change that late slope. The included numerical check verifies this identity to machine precision.

## Numerical results and checks

| Band | N | chi-square, D=2 | chi-square, D=24 | Gain | Gain with twice the scatter |
| --- | ---: | ---: | ---: | ---: | ---: |
| g | 23 | 56.12 | 8.99 | 47.13 | 14.39 |
| r | 25 | 73.33 | 11.34 | 61.99 | 19.44 |
| i | 24 | 94.58 | 15.81 | 78.77 | 33.23 |

With the normal scatter there are no simulated gains as large as observed in 1,999 draws in each band (reported tail fraction 0.0005; this is Monte Carlo resolution, not a precise probability). With doubled scatter the counts are 3, 1 and 0. These tests hold the best UV template fixed.

We separately change its decay time to the source marginal 95-percent endpoints, 11.6307 and 15.1439 days. Even at the longer input decay, the gains are 20.13, 37.78 and 51.82 with normal scatter. This is a sensitivity test, not full joint posterior propagation. Halving the delay grid to 0.25 day changes the D=2 minima by less than 0.004 and the D=24 minima by less than 0.034.

We remove each observing night in turn, and also remove the whole local deficit within two days of the X-ray linear-clock reference. Across all these removals, the smallest gains are 27.90, 32.74 and 50.44 with normal scatter; with doubled scatter they are 8.72, 10.45 and 21.55. Thus the gain is not due only to one night or to the pre-rise deficit. These are fit-cost checks; no tail probabilities were calculated for these variants. Full profiles and checks are in the CSV and JSON files.

## Interpretation and limits

A long positive response can reproduce a fast rise followed by a slow red decline. The data therefore allow an optical response that has both prompt and delayed parts. But positivity alone does not establish such a response physically. Cooling at one emitter can also change the band shapes, and the published thermal evolution makes that possibility relevant. A separate, unobserved central heater can have a different light curve from UVW2. Linear reprocessing of that heater is not excluded here.

The conditional short-response failure does not show which process sets the X-ray dip, why the recurrence changes, or whether the rise-to-dip delay stays fixed. It does show why a physical clock model should fit the emission profiles as well as their markers. A short rise lag and a long decay can coexist; they must not be replaced by one inferred light-travel time.

The main limits are one selected on-state flare, sparse UV sampling represented by a fitted template, a constant optical host, fixed per-band white scatter and no correlated frame or night noise. The bands share observation and calibration effects. The test uses a sampled response grid. A finer-grid check supports the numerical result but is not a proof over continuous kernels. The support profile is not a confidence interval on D. The long response weights are poorly determined, and unobserved tails cannot be recovered. The full UV-to-optical physical relation can be nonlinear or time dependent. We did not reduce the raw images again or claim new telescope observations.

## Reproduction

Python 3.12, numpy, pandas, scipy and matplotlib, plus the configured SCI CLI, are sufficient. Run from the unpacked publication:

```
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py /path/to/campaign /path/to/local_scratch --out /path/to/local_results --bootstrap 1999
```

The script verifies the source ZIP, retrieves the two verified files through `sci read`, records their hashes, and writes all new outputs to the requested results directory. Keep scratch and results outside the signed publication. Compare `support_profile.csv`, `bootstrap.json`, `robustness.csv` and `checks.json`; package versions are in the latter. Regeneration takes seconds to minutes on one CPU. No running service or private worktree file is needed.
