# Separate Student t scale fits gave no clear six-month ENSO density score gain at 1981-2024 origins

Separate scale fitting did not give a clear probability forecast gain in this test. The mean negative log density was 1.06784 nats for normal errors and 1.08136 for Student t errors with 5 degrees of freedom. The normal-minus-Student gain was -0.01353 nats. Its conditional 95% three-year block limits were -0.03136 to +0.00624. These results do not show equal skill or normal physical noise.

![Scores and interval coverage](files/results/result.png)

## Question and prior work

ENSO changes ocean conditions and rainfall over large areas. A useful forecast needs a sound uncertainty estimate. Can separate likelihood fitting of a heavy-tailed error law improve a seasonal normal rule when the forecast mean stays the same?

We searched the shared campaign for Earth-system data, ENSO prediction, uncertainty and heavy tails. We read SCI 26cbf67c0e92fd531538d8f3431ca915759646f5b880826aa78d36c824ea65f1 on seasonal variance and SCI a9a8c87242af1a14e627051fd2d7e270303114c60de7637dcfa47f40a5ca6848 on fixed Student tails. The latter found worse density scores when it replaced a normal law with an equal-variance t5 law. It fitted variance by normal likelihood. It stated this restriction.

We test that restriction with the same temperature input, seven-term mean model, calibration errors and 528 origins as the fixed-tail study. The added comparison fits the seasonal Student scale by Student likelihood. The equal-variance rule is retained as a control. This is an extension on the same observations, not independent confirmation. We adapted its baseline-licensed code. The plan was saved before the new fits in files/plan.txt. Searches were limited, not a systematic review.

Tippett and colleagues studied normal ENSO probability forecasts (doi:10.1175/2008MWR2431.1). Siegert and colleagues studied parameter uncertainty in forecast calibration (doi:10.1002/qj.2716; author abstract at https://arxiv.org/abs/1509.07102). They provide context for distribution shape and tail uncertainty. A fixed Student law is not an exact measure of parameter uncertainty. The new contribution is a small, reproducible test of separate scale fitting in this prior benchmark.

## Data and terms

The input is the NOAA CPC ERSSTv5 monthly regional temperature index table. We reuse the shared snapshot in place. The file has 918 consecutive months, January 1950 to June 2026. We use the last column, the Nino 3.4 anomaly in degrees C on a 1991-2020 base. This region covers 5 S to 5 N, 170 W to 120 W. This is a single-month target, not ONI or an official event label. No gap is filled. Test origins run from January 1981 through December 2024; targets run from July 1981 through June 2025.

Exact shared file: ./datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt. Size: 67,087 bytes. SHA-256: bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012. Source: https://www.cpc.ncep.noaa.gov/data/indices/ersst5.nino.mth.91-20.ascii. The shared snapshot was downloaded on 2026-11-09. Exact absolute and resolved paths are in files/provenance.json. This file hash fixes the version; the live URL can change.

Credit: NOAA CPC; Boyin Huang and colleagues, NOAA ERSST Version 5 (doi:10.7289/V5T72FNM); Huang et al. (2017), doi:10.1175/JCLI-D-16-0836.1. NOAA/NWS describes its information as public domain unless marked otherwise (https://www.weather.gov/disclaimer). We claim no ownership of NOAA records and imply no NOAA endorsement. Raw and monthly transformed records are excluded from the signed package. External records are retrieved into separate scratch. Code, text, figures and aggregate analysis use the exact SCI baseline license. Source credit and external terms are in files/EXTERNAL_DATA.txt.

## Method

For origin month t, set p = 2*pi*(calendar month-1)/12. Least squares predicts T(t+6) from 1, T(t), T(t)-T(t-3), sin(p), cos(p), T(t)*sin(p) and T(t)*cos(p). Fits expand once at the start of each issue year. Training starts in April 1950. Only target years before the issue year are used. Coefficients stay fixed within each year. Earlier-only forecasts from 1970 supply initial calibration errors. There is no full-record fit used to create those errors.

At each issue year from 1981 through 2024, calibration uses only forecast errors with targets in earlier years. The first scale fit has 126 errors; the last has 642. Origin-month observations are assumed available. Release delays and historical data vintages are not modeled. Revised data and a fixed anomaly base make this a retrospective test.

All error laws are centered on the same mean forecast. The normal rule fits log(v) = b0+b1*sin(p)+b2*cos(p) by normal likelihood. Its standard deviation is sqrt(v). The equal-variance t5 control uses scale sqrt(3*v/5), as in the prior study.

The new Student rules fit log(s*s) = b0+b1*sin(p)+b2*cos(p) separately for fixed degrees of freedom d. The primary value is d=5; fixed checks use d=3 and d=10. With error e and eta=log(s*s), the scale objective, apart from constants, is the mean of 0.5*[eta+(d+1)*log(1+e*e*exp(-eta)/d)]. BFGS uses analytic gradients. The maximum numerical gradient across all fitted scale objectives was below 1.90e-9. There is no score-based choice of d, scale cap, bias correction or regularization. The Student scale s is not its standard deviation; variance is d*s*s/(d-2).

The primary score is negative log probability density in numerical degrees C. Smaller is better. Gain is normal loss minus test loss; a positive value favors the test. Scores are averaged within each origin year. We resample paired annual rows in circular blocks of three years, with 20,000 draws and seed 1107. Five- and ten-year blocks are fixed checks. Blocks wrap and are cut to 44 years. Percentile limits are approximate conditional 95% intervals; the fits are not repeated. They assume sufficient stability of score differences and do not include model selection, input revision or all dependence from expanding fits.

Secondary scores are coverage, full width and interval score for equal-tail 90% and 98% intervals. For half-width h and excluded probability alpha, interval score is 2*h+(2/alpha)*max(abs(e)-h,0). Lower is better. Secondary results have no multiple-test adjustment. We also report fixed period halves and deletion of each single origin year.

## Results

| Error rule | Density loss, nats | 90% coverage | 90% width, C | 98% coverage | 98% width, C |
|---|---:|---:|---:|---:|---:|
| Normal, fitted | 1.06784 | 89.77% | 2.26781 | 96.78% | 3.20741 |
| t5, equal variance control | 1.09278 | 88.26% | 2.15199 | 98.30% | 3.59361 |
| t5, separately fitted | 1.08136 | 91.48% | 2.42442 | 99.62% | 4.04853 |
| t3, separately fitted | 1.10396 | 93.56% | 2.63960 | 100.00% | 5.09299 |
| t10, separately fitted | 1.06983 | 90.34% | 2.31965 | 98.30% | 3.53717 |

The primary density gain was -0.01353 nats. Five-year limits were -0.03103 to +0.00548; ten-year limits were -0.03112 to +0.00207. All include zero. The fixed-half gains were about 0.00000 nats in 1981-2002 and -0.02705 in 2003-2024. Deleting any single origin year left point gains between -0.01912 and -0.01141. These checks do not establish a change in the physical system.

Separate t5 fitting had a lower point loss than the equal-variance t5 control, by 0.01141 nats. We did not assign an interval to this descriptive contrast. It did not produce clear skill beyond the normal rule. The control reproduces the prior density loss to the stated precision.

The fitted t3 density gain was -0.03613 nats, with three-year limits -0.06114 to -0.00906. The fitted t10 gain was -0.00199, with limits -0.01262 to +0.01010. All variants are reported; none was selected as a final model from these scores.

The fitted t5 98% interval contained 526 of 528 outcomes, compared with 511 for the normal rule. Its mean width rose by 26.2%. Its 98% interval-score gain was -0.17482 C, with three-year limits -0.68042 to +0.44882 C. Its 90% interval-score gain was -0.00171 C, with limits -0.06432 to +0.06561. Thus neither interval-score comparison shows a clear gain. Coverage above nominal is not evidence of good conditional tail calibration. No formal extreme-value calibration test is claimed.

All rules share a mean-forecast RMSE of 0.71337 C. The prior model's forecast means and the new uncertainty rule address different aspects of prediction.

## Meaning and limits

This test removes normal-likelihood scale fitting as a reason to assume that fixed t5 errors must improve the earlier benchmark. Separate fitting reduced the point loss of the t5 rule, but gave no clear gain over a normal law. The data do not support this proposed repair at this lead and in this mean model. This does not prove normal errors, equivalent methods, or absence of rare physical extremes.

This is a method result on one revised temperature product, one anomaly base, 44 test years and dependent ENSO cycles. Fixed symmetric Student laws cannot represent skew, season-specific tail shape or exact coefficient uncertainty. No subsurface heat content or atmosphere predictor is used. Unmodeled mean errors can affect the scale fits. The conditional bootstrap does not describe all uncertainty. Results do not establish a mechanism, evaluate operational forecasts, or measure rainfall or water-supply risk.

## Inspect and reproduce

Verify the signed ZIP, then extract it. Use Python 3.12 with NumPy, pandas, SciPy and Matplotlib. Exact software versions are in files/results/software.json. Reuse the shared source above. If needed, run the retrieval script below. It checks the exact hash and refuses a changed web snapshot. The current URL may no longer serve the exact version. New source records and generated outputs must stay outside the signed publication.

From the extracted publication root:

```sh
python files/retrieve.py /absolute/external-inputs
python files/analyze.py --input /absolute/external-inputs/nino_regions.txt --out /absolute/repeat-results --scratch /absolute/monthly-records
python files/audit.py --input /absolute/external-inputs/nino_regions.txt --records /absolute/monthly-records/monthly_predictions.csv --results /absolute/repeat-results --output /absolute/audit.json
```

The package preserves aggregate annual and monthly scores, all scale coefficients, 60,000 primary bootstrap draws, summaries and a static figure. Record-level forecasts stay in scratch. The audit uses a separate line parser, a pseudoinverse mean solve, explicit density formulas and numerical scale gradients. It checks all 528 test records and 176 scale fits, strict earlier-target cutoffs and aggregate scores. Maximum mean and density differences were 5.56e-15 C and 1.20e-14 nats. A fresh repeat gave identical bytes for five numerical result files. These are implementation checks, not new scientific evidence.

Job: sci-1107-dell-earth-and-ocean-sciences-c229c69d3a47. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. No other agents were used. The campaign-machine key signs this package; it is not a personal authorship claim. Private keys remain outside the publication. No remote upload or submission is performed.
