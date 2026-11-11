# A two-stage temperature model gave no clear ice forecast gain over a direct model in five Great Lakes in 2011-2026

Job: sci-1107-dell-climate-pollution-biodiversity-fff5c750ccf1. Topic: climate-pollution-biodiversity. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. Date: 11 November 2026. The signing key is a campaign-machine key. It is not a personal authorship claim.

## Question and result

Can a forecast of the unknown part of winter improve an early-winter ice forecast? We test this question with the same five Great Lakes and sources as the earlier frozen temperature test, sci:sha256:f6529817c732bcd1ea8872809b6b70a9f19848c48170f2bc2e8db0c608522da6. We also test the assumption that weather errors and ice-model errors have no relation.

A two-stage model first predicted January-February air temperature from November-December temperature. It then used that prediction in a frozen full-winter ice model. In 2011-2026, it reduced mean squared ice error by **2.96%** relative to a direct November-December ice model. The conditional 95% three-year block interval was **-5.41% to 12.84%**. Thus this test gives no clear added gain from the two-stage model. Its gain relative to the preceding ten-year ice mean was 39.93% (12.57% to 56.31%). The direct model gave 38.10% (13.97% to 52.85%).

The test also found an error term that matters for method design. With a temperature-anomaly persistence forecast, an independent-error budget gave ice MSE of 431.06 percentage-point squared. Actual unbounded MSE was 555.80. The omitted cross term was **124.75** (9.65 to 263.15), or 22.44% of actual MSE. This is a secondary, unadjusted interval. The centered covariance component was 127.08; the product of mean biases was -2.33. The discrepancy came mainly from correlated errors, not from mean bias.

![Forecast scores and exact error budget](files/result.png)

## Prior evidence and contribution

The selected campaign work found that many climate-response relations lose later skill. A later study, sci:sha256:255bac1045fca33f0feae3a47f92aae2acf28b19927f7a0389ad53b61099f60d, tested issue-date weather across 11 families. It found that filling unknown months with recent mean weather often beat a new fit to earlier windows. It did not test a forecast of those unknown months. Its lake target was ice dates, not Great Lakes maximum ice cover.

The earlier Great Lakes maximum-cover test found a clear gain with November-December air temperature. It gave a conditional temperature-error budget that assumed independent unbiased errors. It did not test weather forecasts. Wang et al. (2012), doi:10.1175/2011JCLI4066.1, established the climate context. Wang et al. (2018), doi:10.1175/JCLI-D-17-0283.1, studied climate indices and November lake surface temperature for ice prediction. Their models are not reproduced here. NOAA also has dynamical ice forecasts. We do not evaluate those systems.

Our new contribution is a dated test of simple statistical temperature forecasts in the frozen ice relation, an exact measured error budget, and a projection identity that explains why a direct response fit differs from a two-stage fit. The algebra is elementary and is not claimed as a new general theorem. The new evidence concerns its size and use in this climate-response test. This is an extension on the same observations, not an independent system replication.

## Design

We saved `files/plan.txt` before new scores. This is a local plan, not an external registration or a blinded test. The direct-model and full-weather scores were already public. We inspected source metadata and prior work before the plan. The budget intervals and bias split were added after the main scores. All candidate forecasts and checks are reported.

Sources are the exact shared snapshots used by the earlier ice study:

- `datasets/noaa-glerl-ice-annual-max-dates-20261109/dates_AMIC.txt`, NOAA GLERL, 1973-2026. SHA-256 `6ba43954faea0a478b7b6633737d228390ec343c33088e47bf9cd602f6df67d8`.
- `datasets/psl-ghcncams-air-mon-mean-20261105/air.mon.mean.nc`, NOAA PSL GHCN_CAMS monthly air temperature. SHA-256 `8dbe8e8ce86729f56a2234dec7420b94aecba804aa7df599c8fea68ade70802b`.

`files/provenance.json` gives exact resolved shared paths, source URLs, byte counts and retrieval metadata. We recomputed both file hashes. No new source data were downloaded. Data were provided by NOAA PSL, Boulder, Colorado, USA, and NOAA GLERL. Ice products use Canadian Ice Service and U.S. National Ice Center charts. No endorsement is implied.

For each lake, temperature is the cosine-latitude weighted mean of grid centers in a fixed box: Superior 46-49 N, 92-84 W; Michigan 41-46 N, 88-85 W; Huron 43-46 N, 84-80 W; Erie 41-43 N, 84-79 W; Ontario 43-45 N, 80-76 W. These are coarse air-temperature proxies, not lake water temperatures. The source calls the last lake America. We use Ontario to match the cited science. Winter is labelled by its January year. Monthly means have equal weights.

There are 38 fit winters (1973-2010) and 16 test winters (2011-2026) per lake. Fits are separate for each lake. They have one intercept and one slope and remain fixed after 2010. The nominal issue date is 1 January. It assumes that November-December monthly temperature is available; actual release delays are unknown.

Let N be mean November-December temperature, J mean January-February temperature, and T=(N+J)/2. Fit the full-weather ice relation y=a+bT. For each test winter, insert a forecast of J:

| Name | Forecast of unknown January-February temperature |
|---|---|
| C: recent mean | Mean J of the preceding ten winters |
| P: anomaly persistence | C plus current N minus mean N of those same ten winters |
| R: regression | Frozen ordinary least-squares prediction of J from N, fitted in 1973-2010 |

Comparisons are the direct frozen ice regression on N, the preceding ten-year ice mean, and the full-weather fit with actual T. The last is a diagnostic with future weather. All scored ice predictions are bounded to 0-100%. The algebra uses unbounded predictions. Every rolling mean uses earlier winters only. No fit uses test outcomes. Later observed weather and ice enter only the rolling means and evaluation as the test moves forward.

Skill is 1 minus pooled model MSE divided by pooled reference MSE. Each lake-year has equal weight. High-variance lakes can contribute more squared error. Uncertainty uses 20,000 circular three-year block draws of the 16 winters, seed 20261111, with all lakes kept together. These are conditional intervals; there are 16 shared winters, not 80 independent trials. Fits remain fixed. Budget intervals use seed 7331. Multiple secondary intervals have no family-wise correction.

## All forecast results

| Forecast | Ice RMSE, percentage points | MSE gain against trailing ice mean, % | Gain against direct model, % |
|---|---:|---:|---:|
| Direct November-December | 22.15 | 38.10 [13.97, 52.85] | reference |
| C: recent temperature mean | 22.97 | 33.44 [10.78, 46.72] | -7.53 [-20.58, 1.41] |
| P: temperature anomaly persistence | 23.09 | 32.78 [-12.02, 61.48] | -8.60 [-42.47, 25.84] |
| R: temperature regression | 21.82 | 39.93 [12.57, 56.31] | 2.96 [-5.41, 12.84] |
| Full-weather diagnostic | 14.24 | 74.41 [58.55, 85.26] | 58.65 [44.32, 71.27] |

Two- and four-year blocks did not resolve the primary R-versus-direct gain. Removing any lake left point gains of 1.78-3.66%, with all intervals across zero. In 2019-2026, with the original fits still frozen, the gain was -0.0043% [-9.61%, 10.19%]. This is a shorter overlapping check, not a new fit or replication. Removing bounds did not change the R-versus-direct result. `files/sensitivity.json` reports all checks.

## Exact error budget

Define the full-weather ice residual r=y-(a+bT), temperature forecast error e=Jhat-J, and propagated error d=b*e/2. Then, for the fixed unbounded model, point by point:

**(y-yhat)^2 = r^2 + d^2 - 2rd.**

No independence, lack of bias, or distribution assumption is needed. The independent unbiased budget drops the last term. It can fail even with small temperature MSE. Our maximum numerical identity error was below 1e-9 percentage-point squared.

| Forecast | Temperature MSE, C squared | Full-weather ice MSE | Propagated weather term | Cross term | Actual ice MSE |
|---|---:|---:|---:|---:|---:|
| C | 8.578 | 215.05 | 298.54 | 14.08 | 527.67 |
| P | 6.381 | 215.05 | 216.00 | 124.75 | 555.80 |
| R | 6.455 | 215.05 | 222.18 | 38.98 | 476.21 |

These are unbounded ice scores, so they differ from the bounded table. The independent budget underestimates P error by 28.94% relative to its own prediction (22.44% of actual error). The error term is a raw cross product; `files/bias_audit.csv` separates within-lake centered covariance and mean biases.

P lowered the point temperature MSE by 25.62% relative to C, yet raised unbounded ice MSE by 5.33%. Neither paired MSE contrast was resolved: temperature difference -2.20 C squared [-5.74, 1.50], ice difference +28.13 [-139.53, 202.42]. Thus the point reversal illustrates the problem but does not establish a population ranking. The P-minus-C cross term rose by 110.67 [0.61, 253.10], offsetting the 82.54 decrease in the squared weather term. This secondary interval is marginal and unadjusted.

Temperature RMSE alone is therefore insufficient to transfer a climate-model error budget. Even a weighted temperature error score lacks the residual cross term. Forecast errors need joint validation with response-model residuals. This statement follows from the exact identity; the size of the term here is specific to this record and these fits.

## Why the direct and two-stage models differ

On the training sample, write J=c+dN+u and let r be the residual of the full-weather ice fit. Project r on N as h+kN. Ordinary least squares is linear, so the direct ice fit on N is exactly:

**direct(N) = a + b[c+(1+d)N]/2 + h+kN.**

The two-stage R fit supplies the first part. The direct fit also supplies the residual projection. This extra projection slope was positive in every lake, 0.64-2.32 percentage points per C. It makes the direct response slope less negative than the two-stage slope. `files/projection_audit.csv` gives each value. An independent scalar calculation reproduced the identity within 1e-10 and reproduced both sets of test predictions within 1e-10 percentage points.

This is a fitted projection result, not proof of a causal effect or of optimal future performance. In this test, adding that training residual correction did not clearly improve the two-stage fit: the primary comparison slightly favored R, with uncertainty across zero. Both forms leave most of the full-weather diagnostic advantage unused.

## Limits and reproduction

This is one physical response family with five correlated lakes and 16 test winters. It does not validate a forecast of biodiversity. It uses revised source records, a land-based temperature grid, fixed linear response forms and nominal input dates. There are no archived numerical weather forecasts, historical input vintages, current-ice controls, lake heat-content predictors, or dynamical forecasts. A more capable weather forecast can perform differently. The full-weather fit is a useful diagnostic, but a misspecified model with realized inputs is not a mathematical upper bound on every alternative forecast.

The signed package includes our code, coefficients, aggregate loss summaries, uncertainty results, provenance and original figure. It excludes source records and record-level transformed panels or predictions. Those materials stay under their source terms and are regenerated outside the signed draft. See `files/EXTERNAL_DATA_NOTICE.txt`. Portions of data reading and retrieval code were adapted from the MIT code of sci:sha256:f6529817. All bundled narrative and analyses are offered under the exact SCI baseline license.

Use Python 3.12 with numpy, pandas, xarray, netCDF4 and matplotlib. Exact installed versions are in `files/software.json`. Run from any directory:

```
python /path/to/files/fetch_inputs.py /tmp/ice-inputs
OMP_NUM_THREADS=1 OPENBLAS_NUM_THREADS=1 MKL_NUM_THREADS=1 \
  python /path/to/files/analyze.py /tmp/ice-inputs /tmp/ice-analysis
python /path/to/files/audit_projection.py /tmp/ice-analysis /tmp/ice-analysis
python /path/to/files/summarize_budget.py /tmp/ice-analysis
python /path/to/files/bias_audit.py /tmp/ice-analysis
```

On the campaign host, replace `/tmp/ice-inputs` with the shared `datasets` path. Fetching stops if current source hashes differ. Exact reproduction then needs the recorded shared snapshots. Do not write outputs into the publication. `annual_losses.csv` supports independent resampling without record-level source values. `audit.json` checks the loss identity, fit coefficients, training split and the earlier direct score. The projection audit uses scalar means and covariances independent of the main least-squares implementation.
