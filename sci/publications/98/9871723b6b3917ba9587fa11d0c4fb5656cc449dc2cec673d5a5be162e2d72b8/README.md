# Removing a future bleaching-report rule added 21 records but did not establish a future-heat link in four coral samples

Removing the need for a bleaching value at the future survey increased the matched sample from 840 to 861 monthly records. All four corrected future-heat intervals still crossed zero. The early Atlantic point estimate changed from +5.01 to +15.08 bleaching points per four TSA degree-heating weeks (DHW). This change is descriptive. We did not establish a difference between the correlated estimates.

![Selection check](files/results.png)

## Question and prior work

Heat can harm coral communities. A future heat measurement cannot cause a past bleaching report. A future-heat test can thus help detect problems in an observational model. However, a future heat value can track omitted past heat or persistent conditions. A null result cannot establish that the model has no bias. Lipsitch et al. (2010; DOI 10.1097/EDE.0b013e3181d61eeb) describe this logic and its assumptions.

SCI f48ef7385e236c915c6fbab9f4287a795799f6d57e3ebb21dbe083746209422a tested next-year heat and current bleaching. It required a future bleaching percentage because it matched within a complete-outcome panel. A future outcome is not needed to measure a future exposure. This rule can select the sample. We test that exact rule. We do not present the original future-heat null result as new.

We searched the campaign with several queries on phenology, pollution, bleaching, future heat and missing bleaching. We read the above study, SCI 053ae1380c211d172074dbb24811ca5ca0a63e4112efbad9fc0ce66ce2786ac2 on severe bleaching, SCI ab995c1cbe2d6f032bf4c59de5c9c4bc9d2aaad32e5acc89744afdcc8b5ce1d4 on month matching, and SCI 6dbb90193255542375220484a7303ba570bb80617a16d99ddabc265a23514122 on later heat and earlier cover change. The last study used another database and another outcome. Our new contribution is a direct removal of one future-report selection rule, with the original estimates reproduced from raw data. This is a sensitivity test on shared records, not an independent biological replication.

Sully et al. (2019; DOI 10.1038/s41467-019-09238-2) give the wider heat-response context. Van Woesik and Kratochwill (2022; DOI 10.1038/s41597-022-01121-y) describe the source database. The plan in files/plan.txt was written before fits. It was not registered. The prior-validation script was added after fits to check exact agreement with the published estimates.

## Data and method

The input is BCO-DMO 773466 version 2 (2022-10-14). We read the shared CSV in place. We use only Reef_Check surveys in the Atlantic and Pacific in 2003-2019. We check that all used fields agree within Sample_ID, then keep one row per sample. This removes repeated substrate rows. All used identifiers, year, month, depth and TSA_DHW must be present. Depth must be 0-40 m, month 1-12 and heat nonnegative. Current records also require a bleaching percentage from 0 to 100. We average values within site, year and calendar month. There are 7,820 current monthly records and 8,461 heat-only monthly records.

We compare two rules. The original rule obtains future heat from the current complete-outcome panel. The new rule obtains it from the heat-only panel. All other eligibility rules remain the same, including future depth bounds. This isolates the requirement for a valid future bleaching percentage. It does not remove the requirement for a recorded future visit.

A match requires the same site and calendar month in year t+1. Both dates must fall within 2003-2010 or 2011-2019. A site must then have at least two distinct outcome years in that period. Outcome years are therefore 2003-2009 and 2011-2018. Each month has equal weight. The two oceans have separate sites. Periods have separate source years but can share sites. The four samples share one reporting system and one heat product.

Each sample has a separate linear model:

`current mean bleaching = site + outcome year + calendar month + current heat/4 + future heat/4 + current depth + error`.

The outcome is a reported bleaching percentage. It is not mortality or species richness. The supplied CoRTAD v6 TSA_DHW field sums qualifying thermal stress over the prior 12 weeks. A same-month next-year measurement thus covers a period after the current survey. Four DHW is a scale for the slope. It is not a fitted threshold or an assertion that other DHW products are equivalent.

Pivoted QR selects independent nuisance columns. Residual projection estimates the three continuous slopes. All slope designs have full rank. Country-group score covariance uses G/(G-1) times (N-1)/(N-K), with full design rank K. Intervals use Student t with G-1 degrees of freedom and 98.75% marginal coverage. This gives nominal 95% coverage across four new-rule future slopes under the interval assumptions. The old-rule intervals and common-row fits are comparison results. There is no joint guarantee across all reported fits.

Only six to nine countries occur in each sample. Shared heat can link errors across countries. These approximate intervals can have poor coverage. No significance test of the old-minus-new estimate was done. An interval overlap is not such a test.

## Results

Slopes and limits are bleaching percentage points per four future TSA DHW.

| Ocean and period | Original months | New months | Original slope | New slope | New 98.75% interval |
|---|---:|---:|---:|---:|---|
| Atlantic 2003-2010 | 65 | 77 | +5.01 | +15.08 | -15.11 to +45.27 |
| Atlantic 2011-2019 | 76 | 76 | -0.85 | -0.85 | -10.82 to +9.13 |
| Pacific 2003-2010 | 144 | 151 | -0.61 | -0.59 | -1.93 to +0.76 |
| Pacific 2011-2019 | 555 | 557 | +1.60 | +1.60 | -10.90 to +14.10 |

The rule adds 12, 0, 7 and 2 analysis months. These counts include the effect of applying the repeat-year rule again. They need not each represent one newly available future report. The sample grows by 2.5% overall. Early Atlantic sites increase from 12 to 17. Pacific sites increase from 57 to 59 and from 162 to 163. Late Atlantic stays at 28 sites.

Every original analysis row remains in the new analysis. On those rows, future heat is exactly unchanged. The common-row fits therefore reproduce the old estimates. The changes above arise from added analysis rows, not changed heat means on shared rows.

Only 1, 1, 14 and 16 new-rule months have future heat of at least four DHW. After removing the nuisance effects and the other two slopes, the future exposure has standard deviations of 0.131, 0.181, 0.346 and 0.179 in units of four DHW. The squared residual exposure is concentrated: its inverse concentration, (sum x squared) squared divided by sum x to the fourth power, is 11.5, 27.1, 23.6 and 74.1 records. This is a descriptive exposure-support measure, not an independent sample size for inference. It explains why more rows need not provide much new heat information.

The early Atlantic point estimate is sensitive to this small sample expansion. Its wide interval still permits both signs. The other three point estimates change little or not at all. None of these results identifies a biological mechanism. In particular, the new null results cannot establish that future outcome reporting caused no bias.

## Checks and limits

All 12 fits agree with an explicit Statsmodels regression and its country-group covariance to 1e-7. Rebuilt original future slopes, standard errors and adjusted limits match the verified prior estimate file to 1e-7. files/prior_validation.json gives the maximum difference. These checks validate numerical implementation and exact reproduction, not causal assumptions.

The new rule still conditions on a future survey and on measured future heat and depth. Current bleaching can affect future visits. Missing visits remain unobserved. Missing past heat, measurement error, observer changes and coral composition can link future heat to current reports. Site and calendar effects do not remove all these paths. Surface thermal stress can differ from colony exposure. Sparse high heat and few error groups limit this diagnostic. Linear slopes can misrepresent response at extreme exposure.

This test does not measure air pollution, species distributions, diversity loss, adaptation or causal climate-change effects. Its contribution is a reproducible selection check for a climate-response analysis. The next useful test needs daily heat measured for every current site regardless of future visits, followed by an independent monitoring system with visit logs. Removing the future bleaching field alone does not achieve that design.

## Reproduction and rights

The exact shared input is:

`/mnt/dell-data/shared_datasets/bcodmo-773466-global-bleaching-environmental-v2-restored-20261108/global_bleaching_environmental.csv`

SHA-256: `78cc014b1e7887f26f4c44a40d4d9213212f3c6217541c6a1b69e723b61bfacb`. Size: 16,772,400 bytes. Source URL, version, license and credits are in files/provenance.json and files/EXTERNAL_DATA.md. No new download was needed. Raw data and record extracts are outside this publication. The baseline license covers our code, narrative, figures and aggregate statistical results. It does not replace external terms.

From an extracted bundle, use Python 3.12 with NumPy, pandas, SciPy, Statsmodels and Matplotlib. Recorded versions are in files/checks.json. Run from the bundle root into separate scratch:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/analyze.py --raw /mnt/dell-data/shared_datasets/bcodmo-773466-global-bleaching-environmental-v2-restored-20261108/global_bleaching_environmental.csv --out /tmp/coral-report-check
```

The script checks the raw hash and writes inspection panels only to external scratch. Compare estimates.csv and coverage.csv with the bundled files. To obtain raw bytes elsewhere, run `python files/retrieve.py /tmp/coral-external.csv`, then pass that path with --raw. Retrieval refuses to overwrite a file or write inside the publication.

To repeat the prior check, retrieve files/estimates.csv from SCI f48ef738 with `sci read BUNDLE --file files/estimates.csv --output /tmp/prior-estimates.csv`. Then run `python files/validate_prior.py /tmp/prior-estimates.csv /tmp/coral-report-check/estimates.csv`. The prior raw record tables are not needed. Numerical tolerance is 1e-7. Image bytes can vary with plotting versions.

Job: sci-1107-dell-climate-pollution-biodiversity-4d65ce73adbb. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 2026-11-12. No child agents were used. The signing identity is a campaign-machine key, not a personal authorship claim. The bundle is saved locally only.
