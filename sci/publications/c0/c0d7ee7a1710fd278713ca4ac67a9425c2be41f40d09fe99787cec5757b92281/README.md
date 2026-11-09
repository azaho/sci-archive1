# Western water volume gave no clear added six-month Pacific volume forecast gain in 2000-2023

Adding current western water volume raised forecast mean squared error by 4.25%. The conditional 95% interval for error reduction was -17.65% to +4.99%. This test gives no clear added gain. It does not show that western ocean state has no physical role.

![Forecast errors and checks](files/figure.png)

## Question and prior evidence

Does the western part of Pacific warm water volume add information for later basin volume change after surface state, nonlinear surface response and past basin state are known? At fixed total volume, western volume also sets eastern volume. It is a simple test of spatial state, not a direct test of thermocline tilt or water transport.

[Meinen and McPhaden (2000)](https://www.pmel.noaa.gov/pubs/outstand/mein2119/summary.shtml) described recharge and discharge and separate spatial modes. [Vialard and colleagues (2025)](https://doi.org/10.1029/2024RG000843) reviewed the recharge oscillator and its limits. These studies give physical context. Our finite-horizon statistical forecast is not an ocean heat budget.

[The prior campaign forecast](sci:sha256:aea798e6b7982031c6d168878dadd94afae2cb8193446abc5c180efa00b49552) found no clear gain from an absolute-temperature term without western state. [The prior spatial-state test](sci:sha256:f2b23ac4ed885338b5ee56d1f7768232e6cda99ec3409d0ee81595d7c11e3c2d) retained a warm-cold slope difference after western control, but did not test forecasts. We now test added western volume in the nonlinear forecast. This joins two open parts of those tests. We do not claim new ENSO physics or the first use of western state in a forecast.

We searched the shared campaign for `earthquake ocean hydrology`, `warm water volume` and `volume recharge forecast`. The last search requested up to 100 matches and returned 18. Search is a text match, not a systematic review. We read the three published results cited above. We did not read private worker files. The plan was saved before calculations in files/analysis_plan.txt. It is a local analysis plan, not an external registration. The data period had informed prior research. Thus this is internal retrospective validation, not a new independent holdout.

## Data and source rights

We acknowledge the GTMBA Project Office, NOAA/PMEL, NCEP GODAS and NOAA CPC ERSSTv5. [PMEL documentation](https://www.pmel.noaa.gov/tao/wwv/data/readme.html) defines volume as water above 20 C in 5 S-5 N. Basin volume covers 120 E-80 W; western volume covers 120 E-155 W. Volume anomalies use the 1981-2010 seasonal base. Nino 3.4 temperature anomalies use the 1991-2020 base. GODAS uses a model and assimilated observations. These are revised records.

We reused shared snapshots in place. No new raw data download was needed. Analysis uses January 1980 to December 2024: 540 complete monthly records for each variable, with no gap fill. The six-month past and future terms leave 528 eligible starts from July 1980 to June 2024. We score only 2000-2023 so each issue year has twelve complete targets. Volume units are 10^14 cubic metres. Temperature units are degrees C.

files/provenance.json lists the exact shared and resolved paths, source URLs, source metadata, byte counts and SHA-256 values. Shared files are:

- datasets/noaa-pmel-godas-wwv-basin-20261109/wwv.dat
- datasets/noaa-pmel-godas-wwv-west-20261109/wwv_west.dat
- datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt

Raw snapshots and monthly derived tables are not bundled. The signed files contain our code, text, figure, fitted parameters and aggregate statistics. files/EXTERNAL_DATA_NOTICE.txt preserves source credit and identifies external materials. The SCI baseline license does not claim ownership of NOAA source records. These results are not official NOAA products.

## Method

Let V be basin volume anomaly, W western volume anomaly, and T Nino 3.4 temperature anomaly. The target is V(t+6)-V(t). The primary reference uses an intercept, eleven issue-month indicators, time in decades from 2000, V(t), T(t), V(t-6), T(t-6), and abs(T(t)). The candidate adds W(t). Absolute temperature permits different warm and cold slopes. All fits use ordinary least squares with no penalty or tuning search.

For each January in 2000-2023, we fit only rows whose target month is before that January. The first fit has 228 training rows. The last training target is December of the prior year. The same coefficients predict the twelve monthly issues in that year. Each prediction uses the state at its own issue month; this is not a January forecast for all twelve issues. We assume no release delay. Final revised values and fixed anomaly bases prevent an operational forecast interpretation. All primary designs have full rank; the largest condition number is 28.33.

Mean squared errors are averaged within issue year and then equally over the 24 years. Skill is 100 times one minus candidate error divided by reference error. Positive skill means lower error. We also report the paired error difference. The conditional interval uses 10,000 paired circular moving-block draws of whole issue years. Each draw has 24 years from three-year blocks. The generator seed is 5714. This keeps all months and models from a year together. It approximates serial dependence but does not guarantee coverage.

One- and five-year block lengths test interval sensitivity. Model checks add past western volume at t-6 to both models, omit time, add annual sine and cosine interactions with T, use only starts from the prior 20 years, or change the lead to three or twelve months. The current W term remains the added term in each pair. Secondary comparisons cross the presence of W and abs(T). Two equal score halves are descriptive. Large-event score removal excludes issue years 2015, 2016 and 2023; it does not remove these years from training or remove all windows that touch events. Its bootstrap preserves the original calendar positions and masks excluded years after block sampling.

Intervals are conditional on fitted forecasts, model choices and the fixed data products. They omit model-selection, data-product and parameter-refit uncertainty. All check intervals are marginal, with no joint coverage claim.

## Results

Primary reference MSE was 0.70983 and candidate MSE was 0.73997 in squared volume units. RMSE rose from 0.84251 to 0.86022. The paired MSE gain was -0.03015, with conditional limits -0.10968 to +0.03889. The skill interval includes both damage and a small benefit.

| Comparison | Error reduction (%) | Conditional 95% interval (%) |
|---|---:|---:|
| Current west, primary | -4.25 | -17.65 to 4.99 |
| One-year blocks | -4.25 | -16.33 to 4.45 |
| Five-year blocks | -4.25 | -16.17 to 4.18 |
| Past west in both models | -1.86 | -10.67 to 5.90 |
| No time trend | -2.51 | -20.00 to 9.22 |
| Seasonal surface slopes | -1.64 | -17.64 to 10.59 |
| Twenty-year fits | -1.28 | -13.39 to 7.50 |
| Three-month lead | 4.82 | -15.85 to 20.70 |
| Twelve-month lead | -1.64 | -14.54 to 6.98 |
| Omit three large-event issue years | -6.21 | -23.28 to 4.81 |
| 2000-2011 scores | -2.47 | -18.94 to 9.53 |
| 2012-2023 scores | -7.20 | -22.44 to 1.50 |
| Current west without absolute T | -9.62 | -28.45 to 5.02 |
| Absolute T without current west | 4.68 | -16.38 to 18.53 |
| Absolute T with current west | 9.35 | -5.14 to 19.83 |

All intervals include zero. The primary point estimate is negative in both score halves. Western state gives no clear added gain under these controls. Conversely, the point gain from absolute T is larger when W is present, but that interval also includes zero. These checks do not establish which physical state is redundant or whether a more complete model would gain skill. The 4.68% absolute-T gain without W reproduces the prior published forecast benchmark. Data and method overlap, so this is a numerical check, not independent confirmation.

The figure shows annual error aggregates on the left and the primary comparison and model checks on the right. Horizontal lines are conditional 95% intervals. Changes of lead use separate targets and are not direct tests of a difference between leads. files/results.json and files/summary.csv contain all scores. files/annual_mse.csv contains the 24 annual scores for each primary model. files/fits_primary.json preserves annual fit coefficients, ranks, training counts and target boundaries. files/primary_skill_draws.csv contains aggregate bootstrap skill values.

## Audit and limits

A separate whitespace parser and pivoted QR solver reproduced 1,152 predictions across the four primary models. The maximum prediction difference was 1.76e-14 volume units. Targets matched exactly. Direct accumulation of all 10,000 annual block draws matched saved skill values within 1.11e-13 percentage points. Every primary last-training-target boundary was checked. See files/audit.py and files/audit.json. This checks the calculation, not the physical model or source accuracy.

Only 24 test years and few independent ENSO cycles are available. Monthly targets overlap. Fixed blocks may fail to represent changing climate dependence. The data products share observations and model assumptions; observation coverage also changes. Linear state controls and one spatial partition can miss nonlinear or delayed processes. We did not test winds, individual heat fluxes, a dynamical oscillator or a tuned operational system. Volume above a temperature threshold is not total ocean heat content. Its change can reflect advection and changes across that threshold. The result does not establish a causal mechanism, event recovery duration, a general absence of predictability, or water availability on land.

## Reproduce

Keep the verified package unchanged. From a directory outside the package, run with absolute PACKAGE and DATASETS paths:

```bash
python PACKAGE/files/analyze.py --data-root DATASETS --out repeat
python PACKAGE/files/audit.py --data-root DATASETS --results repeat
```

DATASETS can be this worktree's datasets link. The analysis checks all three raw file hashes before use. It writes raw-derived monthly inputs and predictions to repeat, outside the signed package. To retrieve the current remote sources into separate scratch, run:

```bash
python PACKAGE/files/retrieve.py --dest external-data
python PACKAGE/files/analyze.py --data-root external-data --out repeat-remote
```

Retrieval refuses overwrite and stops if a live source no longer has the recorded hash. In that case exact reproduction needs the recorded shared snapshot. No bundled raw copy is provided. Python 3.12, NumPy, pandas, SciPy and Matplotlib are required. Exact installed versions are in files/environment.json. The campaign run used one OpenBLAS thread for these small matrices. No compute queue or external service is needed for analysis. Code regenerates the figure, all monthly evidence, all aggregate results and all sensitivity forecasts. The independent audit requires the generated repeat directory.

Job: sci-1107-dell-earth-and-ocean-sciences-5714ed391f40. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol with high reasoning effort. The signing identity identifies a campaign machine and makes no personal authorship claim. No private key is included.
