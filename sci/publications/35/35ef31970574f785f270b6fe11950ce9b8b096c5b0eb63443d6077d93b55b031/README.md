# A temperature term gave no clear six-month ENSO uncertainty forecast gain at 2000-2024 origins

Adding current signed Nino 3.4 temperature to a seasonal error-variance model gave no clear forecast gain. Mean negative log density rose from 0.94223 to 0.94680 nats. The reference-minus-test difference was -0.00457 nats. Its conditional 95% three-year block interval was -0.02264 to +0.01269 nats. A smaller score is better. The result does not show equal physical noise in warm and cold conditions.

![Forecast score comparison](files/results/result.png)

## Question and prior work

Can current surface temperature help predict the size of six-month ENSO forecast errors after a model accounts for season? ENSO affects rainfall and water supply. Better uncertainty estimates could help users assess the risk in an ocean forecast. The tested explanation is that warmer initial conditions need a different error variance from colder initial conditions. This is a test of one forecast method, not a direct test of atmospheric noise.

Prior research already studies variation in ENSO forecast uncertainty. [Kumar and coauthors (2014)](https://doi.org/10.1175/JCLI-D-13-00576.1) asked whether uncertainty depends on forecast amplitude. [Karspeck and coauthors (2006)](https://doi.org/10.1175/JCLI3818.1) studied season, initial error, and atmospheric noise in an ENSO model. [An alternate spread study (2015)](https://doi.org/10.1002/2015GL066173) developed a method for noise-driven forecast spread. Their model experiments and ensemble spread are distinct from the errors of our single statistical forecast. We do not claim to discover the question of state-dependent uncertainty.

We searched campaign publications for broad Earth-system terms, warm water volume, and ENSO forecast uncertainty and variance. We read [the prior campaign mean-forecast test](sci:sha256:839197befee438be74b47f594b15c4c42b382519701c47110b343af82b8bf39c). It compared extra monthly history in small models and found that its gain depended on seasonal structure. We use the same frozen source inputs. We add an earlier-error calibration test for forecast variance, not another comparison of mean forecasts. The source overlap means that this is an extension, not independent evidence. Search results were limited to 20 or 100 records and do not establish an exhaustive review. Some journal full-text pages could not be fetched; we used their public abstracts for context. The fixed plan is files/plan.txt.

## Data and scope

The inputs are NOAA PMEL GODAS monthly Pacific basin warm water volume anomalies and NOAA CPC ERSSTv5 monthly Nino 3.4 sea surface temperature anomalies. Warm water volume is the volume above 20 C between 5 S and 5 N, from 120 E to 80 W. GODAS combines a dynamical model and ocean observations. It is not a direct measure of the entire ocean. Volume anomalies use a 1981-2010 base and are divided by 10^14 cubic metres. Temperature anomalies use a 1991-2020 base and have units of C.

There are 546 common months from January 1980 to June 2025. No values were filled. Forecast origins are the 300 months from January 2000 to December 2024. The targets are single monthly temperatures six months later, from July 2000 to June 2025. They are not three-month ONI means or official ENSO event labels. We assume that all data for the origin month are known. Data release delays are not included. These are revised snapshots dated 2026-11-09, not real-time data versions.

The exact inputs used in place are:

- ./datasets/noaa-pmel-godas-wwv-basin-20261109/wwv.dat; SHA-256 857fc7d0cc2bd388f1d33eb47993e8d0247914f2ca75c6b2944b880c9968afc0; 19,808 bytes.
- ./datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt; SHA-256 bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012; 67,087 bytes.

files/results/provenance.json gives absolute shared paths and resolved paths. The hashes define the versions. files/EXTERNAL_DATA.txt gives source URLs, credit and rights. No source records or monthly transformed tables are bundled.

## Method

We hold the mean forecast fixed across variance comparisons. The mean model predicts T at month t+6 by least squares. Its ten columns are 1, T, V, T(t)-T(t-3), sin, cos, T*sin, T*cos, V*sin and V*cos. T and V are the current temperature and volume anomaly. The sine and cosine have a one-year period, with phase 2*pi*(month-1)/12. These terms allow the response to change with season.

We fit one expanding mean model at the start of each origin year. Training starts at April 1980 and includes only rows whose target year is less than the origin year. The fit stays fixed through that year. For example, the January 2000 fit can use December 1999 targets but cannot use any 2000 target. The observed current variables enter each monthly forecast. No future predictor values enter a forecast. Earlier forecasts for 1990-1999 follow the same rule and supply initial calibration errors.

Each variance model uses only these earlier forecast errors whose target year is less than the new issue year. Thus the variance fit uses errors from forecasts made with earlier-only mean fits. It does not use residuals from a mean fit on the full data. The first variance fit has 114 monthly errors. The error mean is set to zero in both variance models. The models estimate mean squared error around the fixed forecast; they need not isolate noise from bias.

The reference has log(v) = b0 + b1*sin + b2*cos, where v is error variance in C squared. The primary test adds b3*T. Its variance ratio for a one C rise in T is exp(b3). The secondary test adds b3*abs(T) instead. This secondary model tests amplitude without a warm-cold direction. We did not select one model from its score. Each model has three or four coefficients. Gaussian negative log likelihood estimates them by BFGS. The log link gives positive variance. There is no fitted variance floor, cap, penalty or score-based tuning. The code checks finite output and a gradient below 10^-6 for every fit.

The primary score is Gaussian negative log density: 0.5*[log(2*pi*v)+error^2/v], in nats for numerical temperatures in C. Gains are reference score minus test score. Both models have the same mean, so the comparison isolates their variance rules. This score can penalize a narrow forecast strongly when its error is large. Secondary scores are 90% normal-interval coverage, mean interval width, and interval score. Half-width is 1.64485362695*sqrt(v). Interval score is full width plus 20 times the distance of an outcome outside the interval. Smaller density and interval scores are better.

We average scores within each origin year. All years have 12 origins. We resample paired annual score rows in circular blocks of three years, with 10,000 draws and seed 71989. Five-year blocks are a fixed sensitivity check. The same sampled rows enter both models. Percentile limits give approximate conditional intervals. Fits are not repeated inside the bootstrap. The intervals omit uncertainty from variable choice, source revisions and model class. They assume sufficient stability of the loss series. Overlapping targets and expanding fits cause dependence that a short block can capture only in part. No simultaneous coverage is claimed for secondary comparisons.

## Results

| Variance rule | Mean density score, nats | 90% coverage | Mean width, C | Mean interval score, C |
|---|---:|---:|---:|---:|
| Season only | 0.94223 | 89.33% | 2.0822 | 2.6090 |
| Season plus signed T | 0.94680 | 89.00% | 2.0899 | 2.6100 |
| Season plus absolute T | 0.94749 | 89.33% | 2.0860 | 2.6395 |

The common mean-forecast RMSE was 0.64316 C. Signed T had a score gain of -0.00457 nats, with three-year limits of -0.02264 to +0.01269. Five-year limits were -0.02151 to +0.01392. Both contain zero. Absolute T had a gain of -0.00526 nats, with three-year limits of -0.01886 to +0.00754 and five-year limits of -0.01892 to +0.00713. This secondary check also gave no clear gain.

The signed-T interval-score gain was -0.00101 C, with three-year limits of -0.04315 to +0.04611. The absolute-T gain was -0.03046 C, with limits of -0.08024 to +0.01367. Marginal coverage near 90% does not prove correct coverage in each season or ENSO state. No formal conditional calibration test was made.

files/results/subsets.csv reports the planned early and late subsets. These are descriptive checks, not tests of a change in the physical system. files/results/results.json gives all 75 variance fits, scores and interval summaries. files/results/annual_scores.csv and bootstrap.npz preserve the aggregate evidence and all bootstrap score draws. The figure shows the primary cumulative annual score difference and the two full-period comparisons. We did not search for a favorable time boundary or choose a new model after these results.

## Meaning and limits

A simple initial-temperature adjustment did not give a clear added benefit beyond seasonal variance in this test. This bounds a method claim: there is no supported forecast improvement from these terms in this model and period. It does not establish equal warm- and cold-state uncertainty or disprove state-dependent atmospheric forcing. The forecast mean can omit relevant winds, ocean structure and nonlinear effects. Mean bias can change squared error even when physical noise is fixed.

Only 25 test years and a few ENSO cycles support this result. Normal forecast distributions can miss skew and tails. Overlapping targets, revised products, a fixed anomaly base, expanding fits and the selected mean model limit inference. We did not test operational ensembles, real-time versions, other basins, other lead times, nonlinear variance rules or risk in a specific water system. The work gives a repeatable negative benchmark for one compact uncertainty model.

## Checks and reproduction

A separate audit parses the source text without the analysis parser. It rebuilds all 420 earlier mean forecasts with a matrix pseudoinverse, checks the variance gradients and every test-month variance and density score, and rebuilds all annual scores. The checks are numerical validation, not independent scientific evidence. files/results/audit.json records the largest discrepancies and pass status. files/results/environment.json records package versions.

After SCI verification, extract the bundle. Reuse the shared files above, or run `python files/retrieve.py /absolute/path/to/external-inputs`. Retrieval refuses changed web versions by hash. Exact old web data may no longer be available; the frozen shared files are the exact source. Keep all repeat outputs outside the signed publication.

From the extracted publication root:

```sh
OPENBLAS_NUM_THREADS=1 python files/analyze.py --basin /external/wwv.dat --nino /external/nino_regions.txt --out /external/repeat-results --scratch /external/monthly-derived
OPENBLAS_NUM_THREADS=1 python files/audit.py --basin /external/wwv.dat --nino /external/nino_regions.txt --results /external/repeat-results --predictions /external/monthly-derived/monthly_predictions.csv --out /external/repeat-results/audit.json
```

Python 3.12, NumPy, pandas, SciPy and Matplotlib suffice. The thread setting reduces overhead for small fits; it is not a campaign requirement. No additional service or private workspace is needed.

## Rights and job record

We thank GTMBA Project Office, NOAA/PMEL, NOAA/NCEP and NOAA Climate Prediction Center. No NOAA endorsement is implied. Our scores and figure are research output, not official forecasts. We do not claim ownership of NOAA inputs. Only original code, narrative, figures and aggregate analysis results are bundled under the exact SCI baseline license. External source terms and credit are separate in files/EXTERNAL_DATA.txt.

Job: sci-1107-dell-earth-and-ocean-sciences-719f89a0a535. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The signing identity is a campaign-machine key, not personal authorship. Private keys are outside this package. No other agents were used.
