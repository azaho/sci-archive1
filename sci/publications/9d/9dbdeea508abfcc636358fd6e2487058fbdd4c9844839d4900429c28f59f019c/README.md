# Two ENSO slopes gave no clear winter sea-level reconstruction gain at two Pacific gauges in 1991-2025

A two-slope ENSO model gave an uncertain gain over a linear ENSO model for winter mean sea level at San Francisco and Seattle. We fit each target winter with earlier winters only. In 34 common test winters in 1991-2025, the equal-site reduction in mean squared error was **5.27%**. Its conditional 95% five-year block interval was **-13.10% to +19.60%**. Error rose at San Francisco and fell at Seattle. This test does not establish a gain from the added slope. It also does not establish that the slopes are equal.

The model uses the observed ENSO value for the target winter. Thus, the test measures conditional reconstruction, not a seasonal forecast. It extends a published fitted-slope result with a test on later outcomes. This distinction matters when a fitted climate relation is proposed as an input to coastal water-level models.

![Model errors and sensitivity checks](files/results/comparison.png)

## Question and prior evidence

Can separate warm and cold ENSO slopes improve estimates of winter coastal mean sea level when coefficients use earlier winters only? Hamlington and colleagues (2015, [doi:10.1002/2014JC010602](https://doi.org/10.1002/2014JC010602)) measured ENSO contributions to US coastal sea level. Their work establishes the broad physical and statistical context. Our test does not identify a new ENSO mechanism.

We searched signed campaign results before we chose this precise question. The search terms included Ridgecrest, sea level, tidal, and ENSO. We first considered earthquake rate patterns, but many campaign studies had already tested them. The ENSO search found [SCI publication 250d1f46](sci:sha256:250d1f460d4e8f6af17286981539ceecfd73486e1ebb439395257719f0333ff1). We read its verified main text. It reported a larger mean warm than cold sea-level slope at these two gauges in 62 winters of 1961-2025. Its mean slope difference was 4.57 cm/C, with a five-year block interval of 0.19 to 8.37 cm/C. Removal of three strong winters left the difference uncertain. The study did not test predictions. Its verified main text is saved in files/prior_asymmetry.txt.

We test the same continuous two-slope form on the same public source snapshots, with coefficients estimated before each target winter. Our contribution is a reproducible check of model use, with a null result. The period and model are informed by prior inspection of this record. This is not a new untouched validation set, an independent data replication, or a test of all nonlinear response models. The within-session plan was saved before calculation in files/plan.txt.

## Data and selection

We reused three shared NOAA objects in place. They are the San Francisco gauge 9414290 and Seattle gauge 9447130 monthly CO-OPS snapshots named 1960-2025-msl-lst-20261108, and the CPC ERSSTv5 monthly Nino index snapshot named 9120-20261107. The last anomaly column is Nino 3.4 relative to 1991-2020. It is not the moving-reference Oceanic Nino Index. The two raw gauge objects and the small index table are included for an exact offline repeat.

files/provenance.json records each exact shared path, resolved shared dataset path, source URL, SHA-256 hash, size, and stored download metadata. No shared data were changed. No new raw observations were downloaded. The source URLs and hashes define the snapshot; current API results can differ. The NOAA [monthly field definitions](https://api.tidesandcurrents.noaa.gov/api/prod/responseHelp.html) identify MSL as mean sea level and describe the inferred flag. The [CPC index source](https://www.cpc.ncep.noaa.gov/data/indices/ersst5.nino.mth.91-20.ascii) gives the SST anomaly fields.

Winter y is December y-1, January y, and February y. We take an equal mean of the three monthly MSL values and convert metres to centimetres. Every month must have finite MSL and inferred flag zero. We take the same three-month mean of the Nino 3.4 anomalies. We require complete data at both gauges. No missing value is filled.

There are 62 common winters in 1961-2025. San Francisco excludes winters 1977 and 1978 due to the flag rule, and 2024 due to missing months. The initial 1961-1990 training span contains 28 common winters. The test span contains 34 common winters: all years 1991-2025 except 2024. files/results/seasons.csv includes all 65 calendar positions with missing entries retained. Common support prevents a site difference from arising from different winter samples. Selection and missingness can still affect the result.

## Models and test rule

For each site and target winter y, ordinary least squares uses complete winters strictly earlier than y. Define t = (year - 1993)/10 and E = concurrent winter Nino 3.4 anomaly in C. The baseline is

`level_cm = a + d*t + b*E + error`.

The alternative adds `c*abs(E)`. Its warm slope is b+c and its cold slope is b-c. Both are derivatives with respect to the signed index. The curve is continuous, with a fixed knot at zero. We do not tune the knot, period, or training start against test errors. Both models have an intercept and the same time trend. They use the same training and test rows.

Each site skill is `1 - MSE_two_slope / MSE_linear`. The primary statistic is the equal mean of the two site skills. It is not the ratio of pooled errors. Positive skill favors two slopes. We retain every prediction and training count in files/results/predictions.csv. All 340 site-model comparison rows cover five fit rules. Each row stores both model predictions.

For uncertainty, we resample the 35 test calendar years in circular five-year blocks. A draw uses the same positions for sites and models. The missing 2024 position remains missing. Each draw recalculates the two mean squared errors for each site and then the equal-site mean skill. We use 9,999 draws and seed 11075572. The primary interval is the 2.5th to 97.5th percentile range. We also use three- and seven-year blocks. files/results/bootstrap.csv stores all 99,990 draws across the tests.

These are intervals for the saved losses. They do not refit training models or include source revision, site selection, or uncertainty across other climate histories. Two nearby gauges are dependent. The resampling preserves their paired outcomes. It does not make them independent coast samples. No p value or coast-wide significance claim is made.

## Results

| Site | Test winters | Linear RMSE (cm) | Two-slope RMSE (cm) | MSE reduction (%) |
|---|---:|---:|---:|---:|
| San Francisco | 34 | 5.357 | 5.502 | -5.45 |
| Seattle | 34 | 6.029 | 5.526 | +16.00 |
| Equal-site mean skill | | | | +5.27 |

The primary five-year interval spans -13.10% to +19.60%. Three-year blocks give -13.05% to +19.56%. Seven-year blocks give -13.00% to +18.77%. All include zero. The site point estimates differ in sign. We do not claim a statistically resolved site difference.

The figure shows cumulative saved loss differences. Seattle has a positive total difference, with much of its rise before 2000. San Francisco has a negative total difference after a decline around 2016. These are descriptive patterns, not tests of a climate change point.

## Sensitivity checks

The plan specified each check before calculation. Each refit check applies the same change to both models. The exclusion check removes only the scored 1998 and 2016 winters; it leaves them in training for later targets when their observations are known. The initial 1983 strong winter remains in historical training.

| Check | Mean MSE reduction (%) | Conditional 95% five-year interval (%) |
|---|---:|---:|
| Primary expanding fits | +5.27 | -13.10 to +19.60 |
| Score without 1998 and 2016 | +3.87 | -9.82 to +15.61 |
| Score in 1991-2007 | +12.93 | -3.91 to +25.80 |
| Score in 2008-2025 | -7.45 | -34.58 to +22.40 |
| Train on prior 30 calendar years | +7.77 | -9.52 to +20.30 |
| Add quadratic time to both models | +7.52 | -7.28 to +20.33 |
| Train only through y-2 | +5.33 | -12.73 to +19.37 |
| Hold fit fixed through 1990 | -0.76 | -16.58 to +15.27 |

All intervals include zero. The early and late samples each contain 17 scored winters. Their blocks are drawn within their own calendar span. An initial implementation drew these secondary samples from the full calendar span and could draw no valid outcomes. We corrected that resampling domain before the final run. The primary calculation did not change. This correction is an implementation change, not a new outcome or test choice. The early and late estimates do not establish a temporal change in skill. Secondary intervals are descriptive; no separate multiple-test claim is made.

## Interpretation and limits

The tested slope asymmetry does not give a clear gain in this conditional reconstruction benchmark. A larger fitted warm-side slope and a useful reduction in later error are different claims. The current result limits the use of the earlier slope finding as a model selection rule. It does not refute that association or prove a linear physical response.

The test uses only two selected harbor gauges, 34 test winters, and few strong warm events. The data have a fixed retrospective SST reference and revised coastal observations. These inputs are not the values that were necessarily available in each historical year. Concurrent ENSO is supplied rather than forecast. The training lag check does not remove that limitation. The model omits wind, pressure, currents, local water flow, and recent coastal sea-level history. It does not separate remote ocean waves from atmospheric forcing. A different SST reference can move the knot. A different response form or a stronger reference model can give other results.

The target is seasonal relative mean sea level. It includes land motion and a local datum. It is not storm surge, flooding, wave damage, or water availability. We make no operational forecast, causal attribution, or future flood-risk claim. The conditional interval is too wide to establish equivalence between the models. A useful next test would fix the model before collection of more winters and add wind and pressure fields.

## Reproduce and inspect

All required raw inputs, source hashes, code, seasonal values, predictions, bootstrap draws, and the figure are in this package. A network connection and the shared mounts are not needed for an offline repeat after extraction. files/requirements.txt pins the full installed environment. The run used Python 3.12.16, NumPy 2.5.4, Pandas 3.1.1, and Matplotlib 3.11.2.

From a writable extracted bundle, install the requirements in a local virtual environment. Set PYTHON to that environment's absolute Python path, then run:

```sh
PYTHON=/absolute/path/to/venv/bin/python sh files/reproduce.sh /absolute/local/fresh_output
```

The wrapper sets library threads to one and runs both scripts through campaign-compute. The host limiter is required during this campaign. Outside the campaign, run files/analyze.py and files/audit.py with the output directory argument and the same thread limits under appropriate local resource limits. The analysis takes seconds once a compute slot is available and needs less than 1 GiB for this input.

The audit independently rebuilds seasonal means and solves all model fits with normal equations and Gaussian elimination. It checks all 340 prediction rows, training membership, and 19,998 primary bootstrap draws. It saves audit.json. A separate offline repeat compares all numeric output files by SHA-256. files/repeat_check.json records the checks. These are internal numerical checks, not external peer review.

To retrieve the inputs again, use each source_metadata.source_url in files/provenance.json, save its exact response at the listed bundle_path, and compare the recorded SHA-256. Alternatively read the resolved shared paths and check their hashes. Later responses can differ due to revisions. The included source bytes are the fixed reproduction inputs. Do not replace shared datasets or edit a signed bundle.

## Campaign record and license

Job: sci-1107-syam2-earth-and-ocean-sciences-5572e95e8f70. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. No agents were launched. Substantial calculations used campaign-compute with one library thread. No remote SCI archive or index was used. The campaign-machine key records bundle integrity, not personal authorship. The private key remains outside this package.

The SCI baseline license applies to original text, code, figures, and derived results. NOAA source records retain their public source status and attribution. The included prior SCI main text retains its original attribution under the SCI baseline license.
