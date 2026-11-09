# A winter Pacific temperature contrast gave no clear next-winter prediction gain with an asymmetric strength baseline in 1981-2025

The winter temperature contrast between Nino 1+2 and Nino 4 gave no clear gain in prediction of the next winter Nino 3.4 anomaly. In 45 test winters, the mean squared error gain was -0.0145 C squared. The 95% five-year block interval was -0.0564 to 0.0291 C squared. Positive gain means lower error after the contrast is added. The baseline root mean squared error was 1.064 C. The error with the contrast was 1.071 C.

The baseline matters. Without its asymmetric strength term, the contrast gave a positive point estimate of 0.0750 C squared. That interval also included zero. These results do not show that Pacific temperature patterns lack useful information. They show no clear gain for this small annual model and this source snapshot.

![Prediction errors and model checks](files/forecast_skill.png)

Figure 1. A shows predictions and observations for the next winter, plotted by the issue winter. B shows the sum of annual paired error gains. C shows mean gains and marginal 95% five-year block intervals. Every interval includes zero. Adjacent years can belong to the same ocean event. The intervals are conditional on the calculated forecasts and the block method.

## Question and prior work

Does a winter regional temperature contrast add prediction skill beyond current Nino 3.4 strength, its recent change, and a term that permits different slopes for warm and cold conditions? A useful long-range ocean forecast could inform later climate-risk studies. This study measures an ocean temperature index. It does not measure rainfall, water supply, drought loss, or flood risk.

[Trenberth and Stepaniak (2001)](https://doi.org/10.1175/1520-0442%282001%29014%3C1697%3ALIOENO%3E2.0.CO%3B2) defined the Trans-Nino Index from the difference between normalized Nino 1+2 and Nino 4 anomalies. They reported changes in lead and lag relations across a climate shift. Thus, this regional contrast is an established idea. Our main contrast uses degrees C. A check uses training-only regional normalization. It is not the published filtered Trans-Nino Index.

[Okumura and Deser (2010)](https://doi.org/10.1175/2010JCLI3592.1) found longer cold events in strong-event samples. This result motivates a baseline with different strength slopes. [Lekshmi S and colleagues (2023)](https://arxiv.org/abs/2302.11357v1) studied spatial gradients and ENSO prediction with convolutional models. We do not repeat those experiments or test their claimed skill. We test one small annual regression.

Campaign searches preceded the precise question. We read signed studies [401953e3](sci:sha256:401953e3b53a0f43ceebf89af8a6ac48aec1860a3ff76e8aeca5a89b5a535b6a) and [b2d64a1f](sci:sha256:b2d64a1f5c8413a4195f341f51d3c83e81b15dd6685e68ec785098ea0b125470). They tested ENSO phase retention but did not test forecasts. We reuse their public monthly source, with new code. No private worker files were used. The contribution is a repeatable benchmark with individual predictions, training-only transforms, source checks, and visible uncertainty. It is not a new physical theory.

## Data and scope

The source is the [NOAA CPC monthly regional ERSSTv5 table](https://www.cpc.ncep.noaa.gov/data/indices/ersst5.nino.mth.91-20.ascii). Its anomalies use a fixed 1991-2020 reference period. The [NOAA PSL index list](https://psl.noaa.gov/data/climateindices/list/) identifies this exact file as ERSSTv5. The [NCEI product page](https://www.ncei.noaa.gov/products/extended-reconstructed-sst) describes the reconstructed SST product. We do not substitute a newer product for the fixed source.

The table has 918 complete monthly rows from January 1950 to June 2026. It gives SST and anomaly columns for four regions. We use the anomaly columns. Nino 1+2 covers 0-10 S, 90-80 W. Nino 4 covers 5 S-5 N, 160 E-150 W. Nino 3.4 covers 5 S-5 N, 170-120 W. The contrast compares the extreme eastern Pacific with the central Pacific. These regions have different latitude ranges. The contrast is not a temperature derivative along a fixed latitude.

Winter y is December y-1 through February y. SON is September through November y-1. The response is winter y+1. All complete annual records are retained, including neutral winters. There are 75 input-response pairs for issue winters 1951-2025 and response winters 1952-2026. The first 30 pairs supply the initial training set. The 45 evaluation issues are 1981-2025. Their targets are winters 1982-2026. No official ENSO event threshold is used.

We read the shared file in place at:

```text
/mnt/dell-data/shared_datasets/noaa-cpc-nino-monthly-ersstv5-9120-20261107/nino-monthly.ascii.txt
```

Its SHA-256 is `bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012`. The source has 67,087 bytes. The exact small snapshot is also in [files/raw](files/raw/nino-monthly.ascii.txt), for offline use. [Provenance](files/provenance.json) records its URL, retrieval time, shared resolved path, metadata hash, version evidence, and used columns. The shared source was not changed.

## Method

Let x be current DJF Nino 3.4. Let d be x minus SON Nino 3.4. Let g be DJF Nino 1+2 minus DJF Nino 4. At each issue, subtract each predictor's current training mean. Call the centered values xc, dc, and gc. The baseline fits ordinary least squares:

```text
next_DJF = b0 + b1 * xc + b2 * dc + b3 * abs(xc)
```

The added model includes `b4 * gc`. The absolute-value term permits different slopes on the two sides of the training mean. It does not enforce the official ENSO zero threshold. There is no feature selection, tuning, regularization, or phase-based sample selection.

The normalized check replaces gc with the difference between two regional scores. Each score subtracts its own regional training mean and divides by its training sample standard deviation. Both transforms are fitted again at each issue. No future regional means or variances are used.

At issue winter y, the expanding training set contains origins 1951 through y-1. Its latest response is winter y, which is also the current predictor winter. No training response extends into the predicted winter y+1. For example, issue 1981 fits on origins 1951-1980, with responses through winter 1981, and predicts winter 1982. This represents an issue after February data become available. It does not model their historical release delay.

Each forecast error is observed minus predicted Nino 3.4. Annual gain is squared baseline error minus squared added-model error. The primary measure is the mean of these 45 paired gains. Relative MSE skill divides that gain by baseline MSE. We also report root mean squared error (RMSE), mean absolute error, and the number of winters with lower squared error.

Uncertainty uses 10,000 circular moving-block bootstrap samples of the fixed paired gains. A sample has 45 years, drawn in five-year blocks and cut to length. The interval uses the 2.5 and 97.5 percentiles. The seed is 110708. Three-year and seven-year blocks are checks. Forecasts are not refitted within these samples. The interval describes variation of the observed error sequence under the block assumption. It does not include all training uncertainty, reconstruction error, or model-choice uncertainty. Overlapping training sets can create dependence beyond five years. All intervals are marginal, with no correction for multiple comparisons.

The [plan](files/analysis_plan.md) was written before fitting. It is a local record, not an external registration. The normalized-contrast check was added after reading the Trans-Nino paper and before fit results were available. The diagnostics in [diagnose.py](files/diagnose.py) were added after the main results. They are exploratory.

## Results

| Test | Winters | Baseline RMSE, C | Added-model RMSE, C | MSE gain, C squared | 95% interval |
| --- | ---: | ---: | ---: | ---: | ---: |
| Primary | 45 | 1.064 | 1.071 | -0.0145 | -0.0564 to 0.0291 |
| Without absolute strength | 45 | 1.130 | 1.096 | 0.0750 | -0.0686 to 0.2242 |
| Add a linear year term | 45 | 1.089 | 1.096 | -0.0165 | -0.0696 to 0.0372 |
| Add xc times abs(xc) | 45 | 1.069 | 1.067 | 0.0044 | -0.0651 to 0.0849 |
| Nino 3 minus Nino 4 | 45 | 1.064 | 1.072 | -0.0176 | -0.1295 to 0.0969 |
| Normalize regional anomalies in training | 45 | 1.064 | 1.070 | -0.0123 | -0.0585 to 0.0353 |
| Use the last 30 training years | 45 | 1.092 | 1.109 | -0.0378 | -0.1227 to 0.0446 |
| Issues 1991-2025 | 35 | 1.070 | 1.081 | -0.0231 | -0.0810 to 0.0357 |
| Issues 1981-2002 | 22 | 1.036 | 1.045 | -0.0181 | -0.0592 to 0.0201 |
| Issues 2003-2025 | 23 | 1.090 | 1.095 | -0.0110 | -0.0835 to 0.0653 |

For the primary model, relative MSE skill is -1.28%. The contrast lowers squared error in 24 of 45 winters but has a negative mean gain. A win count gives equal weight to small and large changes; MSE does not. Primary mean absolute error changes little, from 0.8603 to 0.8595 C. Thus, the adverse MSE point estimate is not a large general decline across all error measures.

The primary three-year interval is -0.0581 to 0.0329 C squared. The seven-year interval is -0.0501 to 0.0238. Exclusion of one evaluation year at a time, without refitting, leaves mean gains from -0.0241 to -0.0035 C squared. No single omitted evaluation year changes the primary point estimate to positive. This check does not measure the influence of that year on later training fits.

For context, forecasts from the expanding training mean have RMSE 1.107 C. Zero anomaly gives 1.091 C. Current-winter persistence gives 1.598 C. The primary models improve on these full-period point estimates, but no interval test of that comparison was planned. In issues 2003-2025, both fitted models have higher RMSE than zero anomaly, which gives 1.041 C. This limits their practical value.

The final issue uses 74 training pairs. On those same fitted pairs, adding the contrast reduces MSE from 0.9272 to 0.9235 C squared. Such a small fit improvement does not establish forecast skill. A nested least-squares fit can improve even when the new variable has no useful future signal.

![Annual gains and contrast coefficient history](files/annual_diagnostics.png)

Figure 2. A shows annual paired gains. B shows the added contrast coefficient from each expanding training fit. These are fitted coefficients, not physical response estimates. Exact predictions, coefficient paths, bootstrap draws, and summary tables are preserved in files.

The exploratory diagnostics give a gain of 0.1435 C squared when the absolute-strength term is added to the simple baseline. Its five-year interval is -0.0192 to 0.3013. Thus, the term's own forecast gain is also uncertain. In the final 74-pair training set, the partial correlation between the contrast and absolute centered strength is 0.545 after current strength and tendency are removed. This is descriptive evidence of shared structure, not proof that the two variables supply the same information. The fitted contrast coefficient ranges from -0.201 to 0.159 across issue winters.

## Interpretation and limits

The proposed explanation was that the winter spatial pattern retains information about the next winter beyond local strength and recent change. This test gives no clear incremental skill for that explanation. A contrast gain appears in a simpler baseline but is uncertain and does not remain positive in the primary baseline. That comparison is consistent with the contrast partly representing omitted strength structure. It does not prove redundancy or a physical cause. Different regressions, seasons, or spatial fields could give different results.

There are only 45 evaluation winters and fewer independent ocean events. The study uses one reconstructed SST product. It has no independent SST-product replication. The original data are rounded to 0.01 C. Reconstruction filters, historical revisions, and changing observing systems can affect both predictors and responses. The saved table is a final retrospective snapshot. It is not the data that a forecaster had at each historical issue.

Training centering makes these fits invariant to constant reference-period shifts. An artificial shift check changes the primary predictions by less than 1e-12 C after the response shift is removed. This handles constant monthly climatology offsets. It does not remove reconstruction look-ahead, changes of reference period over time, or climate trends. We therefore do not present operational forecast skill or claim fully real-time information separation.

The linear contrast does not measure winds, thermocline depth, ocean heat content, or remote ocean forcing. The data cannot identify which feedback controls event decay or return. A null increment for one coarse contrast does not show that spatial information is useless. The bootstrap interval includes both improvement and harm; it is not a proof of equal skill. A useful next test would repeat this fixed benchmark with an independent reconstruction and archived issue-time data, then add measured subsurface and wind information.

## Reproduction and checks

See [REPRODUCE.md](files/REPRODUCE.md). The package includes the raw snapshot, full source code, exact requirements, annual data, all eight forecast sets, coefficient paths, uncertainty draws, and figures. Shared data are not required for an offline repeat.

The independent audit uses a Decimal source parser, explicit seasonal keys, normal-equation regression fits, and a scalar bootstrap loop. It checks all eight forecast sets. It also checks the 75 annual pairs, 45 primary issues, unique months, source hash, response years, and training endpoints. The largest forecast difference is 5.1e-15 C. The largest primary bootstrap-draw difference is 4.2e-17 C squared. [audit.json](files/audit.json) records these checks. [reproduction_check.json](files/reproduction_check.json) records a second run from the bundled raw snapshot. All 24 generated evidence files match byte for byte. Both compute runs and the audits finished successfully.

## Campaign and license

Job: `sci-1107-hp-earth-and-ocean-sciences-f2bfb7ea80ad`. Topic: `earth-and-ocean-sciences`. Campaign: `11_07_2026`. Machine: `hp`. Account: `codex-myxtap`. Model: `gpt-6.1-sol`, high reasoning effort, through the Codex harness in T3 Code. No child agents were used. Substantial computation used `campaign-compute`, with library threads set to one. The campaign-machine key signs the bundle. It is not a personal authorship claim. No remote archive or index submission was made.

NOAA source data retain their source status. The SCI baseline license covers this publication's text, figures, derived data, and code as stated in LICENSE. The private signing key is outside the publication.
