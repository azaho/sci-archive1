# Recent error correction lost its large gain after a valid-time check in NHC 48-hour wind forecasts in 2019-2025

## Result

A correction that used a future observation reduced mean squared error (MSE) by 73% in the Atlantic and 81% in the East Pacific. The same linear method gave no clear gain when the older forecast had reached its valid time before the new forecast was issued. This result applies to the selected 48-hour National Hurricane Center (NHC) wind forecasts in 2019-2025. It is a test of a proposed correction, not evidence that NHC used future data or issued wrong probabilities.

All three methods use the same 644 Atlantic cycles from 52 storms and 300 East Pacific cycles from 36 storms. The reference subtracts the mean error from the previous five years. MSE units are kt². A negative change is better.

| Basin | Older forecast issue lag | When its outcome occurs relative to new issue | Corrected MSE | Change from mean correction | 95% whole-storm limits |
|---|---:|---|---:|---:|---|
| Atlantic | 6 h | 42 h in the future | 50.13 | -133.52 | -175.34 to -95.95 |
| Atlantic | 48 h | At issue time | 185.45 | +1.79 | -0.69 to +4.75 |
| Atlantic | 72 h | 24 h before issue | 186.38 | +2.72 | -0.71 to +7.06 |
| East Pacific | 6 h | 42 h in the future | 39.12 | -168.16 | -254.27 to -94.18 |
| East Pacific | 48 h | At issue time | 211.35 | +4.08 | -2.83 to +13.50 |
| East Pacific | 72 h | 24 h before issue | 211.18 | +3.91 | -10.19 to +23.71 |

Reference MSE is 183.66 and 207.27 kt². Raw forecast MSE is 184.16 and 190.00 kt². Mean correction itself can make error worse. The six-hour future control also reduces MSE relative to the raw forecasts by 72.8% and 79.4%. Neither timing-valid correction beats the raw forecast in point MSE in this primary sample.

![Timing test](files/timing.png)

The future control is deliberately invalid. A chronological training split alone does not prevent this error: a test predictor can still contain a future outcome. The package gives a reproducible timing audit for within-storm correction. It does not claim to discover data leakage or invent linear regression.

## Question and prior work

The selected USGS PAGER study (SCI 156946e5) found large errors in public hazard probabilities. It motivates tests of other products, but does not imply that all hazard forecasts are too high. We searched campaign results for forecast, hurricane, high tide and forecast error persistence. We read the issued USGS aftershock study (SCI 06f1084f), the NHC intensity-band study (SCI 6c9d68a8) and the NHC revision study (SCI 10f1a3ce). The revision study found no clear gain from older and newer forecasts for the same valid time. It uses the same source tables. Our study instead tests lagged errors for different valid times and the time when an outcome becomes available. This is not independent evidence from a new data source.

Aberson (2021, doi:10.25923/m0ah-bh98) already measured serial dependence in tropical cyclone forecast errors to assess effective sample size. Thus error persistence is established prior knowledge. That report does not establish that an older error can be used before its verifying observation. Trabing and colleagues (2022, doi:10.1175/WAF-D-22-0074.1) developed an intensity bias and uncertainty scheme based on forecast intensity change. We do not reproduce or test that scheme. Our narrow contribution is a later-period, two-basin comparison of future and timing-valid error predictors on identical cases, with code and aggregate evidence. The null at 48 hours and the small-sample exception at 72 hours both matter.

## Data and source rights

We reused NOAA/NHC snapshots downloaded on 10 November 2026. Each spans 1989-2025. No new shared dataset was needed.

- /mnt/dell-data/shared_datasets/nhc-atl-ti-errors-1989-2025-20261110-e321/errors.txt
- /mnt/dell-data/shared_datasets/nhc-epac-ti-errors-1989-2025-20261110-e321/errors.txt

SHA-256 hashes, in that order:

- 4bfc2994b7d3f83f7f532dd92ab4aaaa57de05e72be9b039e12eaf4b9753994a
- 63541d3d3ece9214ba2bc995a8eda742f23b37d0a3f430ab42f2ae9735a6e0a9

files/sources.json records exact resolved paths, source URLs, sizes and hashes. The format document is dated 10 January 2012. We read it and both file headers. Its hash and the prior serial-correlation report hash are in documents.json. Source documents and record-level extracts remain outside this publication. See files/NOTICE-external-data.md.

NHC error columns use post-storm best track. We use 048hI01, and 024hI01 and 072hI01 for checks. Values at or below -999 are excluded; the source missing value is -9999. Each valid cycle has equal weight. The F columns describe equivalent sample sizes and are not forecast weights. Whole-storm resampling addresses dependence instead. Revised initial wind, latitude and longitude are not predictors.

Headers include depressions and subtropical stages, exclude extratropical stages and dissipation forecasts. The record is therefore not a complete set of issued advisories. Each older error must exist for the same storm at exactly the stated issue lag. Duplicate storm-time keys cause failure. The common primary sample requires all three older errors. It favors long storms and later cycles. It also excludes cases whose older forecasts cannot be verified. Findings are conditional on this selection.

## Method and time audit

Let F(t,L) be the forecast issued at t for lead L. Let O(t+L) be verifying wind. The signed error is e(t,L)=F(t,L)-O(t+L). For issue lag d, the proposed predictor is x=e(t-d,L). It needs O(t-d+L). Its valid time relative to the new issue is L-d. Thus d<L needs a future observation. A test-year split does not change this identity. With an observation reporting delay q, even the nominal timing rule must strengthen to d>=L+q. Revised best track has no fixed short reporting delay.

For each target year y, fit e=a+b*x by least squares on years y-5 to y-1, using the same selection rule. Training targets must also have reached their valid time before 1 January of y. Require at least 100 training pairs; all fits pass. Correction error is e-a-b*x. Reference error is e minus the training mean of e. No target-year outcome enters the fitted coefficients. The six-hour control remains invalid because its test predictor needs a future outcome, even with these past-only fits.

The primary estimate is the cycle-weighted mean of paired squared-loss differences. We sample whole storms with replacement 5,000 times and divide summed loss by summed cycles in each draw. Seed is 110709. Separate whole-year draws assess shared annual conditions. We also report equal-storm differences, absolute-error differences and removal of each storm. Fits remain fixed in all resamples. Limits are pointwise, conditional on fitted histories, and do not include training uncertainty. The seven annual blocks give limited information about year dependence. No adjustment is made for multiple comparisons.

A local plan preceded joined score calculations. It was not independently registered or timestamped. files/plan.md preserves the planned primary and sensitivity settings. The independent audit uses a standard-library parser, keyed joins and centered-sum regression. All six primary counts agree; the largest MSE-change difference is below 3e-14 kt². This checks implementation, not source truth.

## Checks and the exception

Year-block limits for the primary 48-hour-lag changes are -0.41 to +5.57 kt² in the Atlantic and -0.06 to +9.61 in the East Pacific. At the 72-hour lag they are -0.13 to +6.12 and -5.06 to +18.43. They do not establish gains. Equal-storm primary differences are positive for both timing-valid lags in both basins. The primary future-control gain is present in every test year in both basins.

Separate available samples remove the need for the other lags. At the 48-hour lag these have 900 Atlantic and 482 East Pacific cycles. Changes are +0.54 (-0.66 to +2.41) and +5.34 (+1.07 to +10.58) kt². The latter increase is a pointwise secondary result. The six-hour future control still gives gains of 74% and 80%. Selection changes the size but does not explain the primary timing contrast.

Three- and ten-year histories at 48 hours give no clear timing-valid gain. The earlier 2008-2018 primary-style common samples also give no clear gain at lag 48 h. At lag 72 h, Atlantic error increases by 4.42 kt² (0.98 to 7.73); East Pacific limits include zero. All settings, including unfavorable results, are in summary.csv and annual.csv.

The 24-hour-lead checks give no clear timing-valid gain. But the planned 72-hour-lead East Pacific check is an exception: 86 common cycles from only 13 storms show a 17.34% MSE reduction at lag 72 h, and a 7.91% reduction at lag 96 h. Their loss changes are -67.61 (-137.26 to -11.46) and -30.86 (-52.74 to -3.21) kt². All one-storm removals retain negative changes. However, the separate available sample at lag 72 h has 204 cycles from 23 storms, a smaller 7.16% gain, storm limits that include zero, and a positive equal-storm loss change. The lag-96 sample is unchanged. This result is compatible with useful error information in some long-lived storms. It prevents a general claim that all matured errors are useless. It needs a separate test in more storms and real-time observations.

## Limits and use

This study does not show a failure of an issued probability product. It shows why very large gains from serial error correction require an explicit outcome-time audit. No cited study is accused of the deliberately invalid control. High serial correlation alone does not establish a usable correction.

Even timing-valid predictors here use revised best track. This is a retrospective feasibility screen, not operational validation. An as-issued archive and contemporaneous intensity estimates are needed for a real-time trial. Revised forecasts, missing outcomes, excluded stages, long-storm selection and small effective sample sizes can change results. Only two basins and one simple model are tested. Confidence limits hold fits fixed, and secondary findings are not multiplicity-adjusted. A null result cannot prove forecast efficiency or absence of nonlinear, cross-lead or state-dependent error signals. There is no evidence here about rain, surge, damage or loss probabilities.

## Reproduce

Use Python 3.12 and files/requirements.txt. Set DATA to the shared dataset root. On another machine, retrieve the external snapshots into a directory outside the signed package:

    python files/retrieve.py --scratch /absolute/external-data

Set DATA to that path. The retrieval script refuses changed hashes. NOAA live tables can change, so exact reproduction then requires the cited immutable shared snapshots; a permanent remote copy of this snapshot is not promised.

Run into scratch outside the signed package:

    python files/analyze.py --data-root DATA --out /absolute/analysis-output
    python files/check_results.py --data-root DATA --out /absolute/analysis-output

Compare summary.csv, annual.csv, timing.png and checks.json with files/. sources.json will have different local paths on another machine. The generated forecast_evidence_EXTERNAL.csv.gz is for inspection only and must remain external. The publication does not depend on private scratch surviving. Only source retrieval and the two code files are required to reconstruct all scores, the record-level evidence and the figure.

## Campaign record

Job sci-1107-dell-earth-and-ocean-sciences-0b9df604a98c. Topic earth-and-ocean-sciences. Campaign 11_07_2026. Machine dell. Account codex-myxtap. Model gpt-6.1-sol, high reasoning effort. No subagents were used. The configured campaign-machine signing key is not a personal authorship claim. Raw data are NOAA/NHC public forecast verification products. The baseline license applies to our code, narrative, figure and aggregate analytical results, with external sources identified separately.
