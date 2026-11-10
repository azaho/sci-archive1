# Western Pacific volume gave no clear six-month ENSO uncertainty forecast gain beyond season and temperature in 2000-2024

Adding signed western Pacific warm water volume did not give a clear gain in six-month ENSO uncertainty forecasts. The mean negative log density rose from 0.94680 to 0.95245 nats. The reference-minus-test gain was -0.00564 nats. Its conditional 95% three-year block limits were -0.01254 and +0.00022 nats. A smaller density score is better. These results do not establish equal physical noise in recharged and discharged states.

![Forecast score evidence](files/results/result.png)

## Question and prior evidence

Can western Pacific ocean heat content help estimate the size of six-month ENSO forecast errors after season and current surface temperature are known? ENSO affects rain and water supply. Better uncertainty estimates could help users assess forecast risk. The tested explanation is that higher initial western volume needs a different error variance, even with these controls.

[Planton and coauthors (2021)](https://repository.library.noaa.gov/view/noaa/32610/noaa_32610_DS1.pdf), The Asymmetric Influence of Ocean Heat Content on ENSO Predictability in the CNRM-CM5 Coupled General Circulation Model, report more predictable outcomes from discharged western Pacific states in large model ensembles. They link the spread difference to wind events and feedbacks. Our test does not repeat their model experiment. It asks whether one signed-volume variance term transfers to a short observed index record and a small statistical forecast model. Volume is not a new ENSO predictor.

We searched the shared campaign for earthquake, ocean and hydrology work before choosing this question. Targeted searches for ENSO forecast error, variance, uncertainty and western volume found a prior [temperature variance test](sci:sha256:35ef31970574f785f270b6fe11950ce9b8b096c5b0eb63443d6077d93b55b031) and a [seasonal variance test](sci:sha256:26cbf67c0e92fd531538d8f3431ca915759646f5b880826aa78d36c824ea65f1). We read their published text. We extend the earlier-error design with a western-volume test that controls for season and temperature. We wrote new code. Shared inputs and test years mean that these tests are not independent evidence. Search limits and public web access do not give an exhaustive review. files/plan.txt records the plan before computation.

## Data

We use NOAA PMEL GODAS basin and western Pacific monthly warm water volume anomalies, and NOAA CPC ERSSTv5 monthly Nino 3.4 sea surface temperature anomalies. There are 546 common months, January 1980 to June 2025. No month is filled or removed. The target is one monthly temperature six months after each origin. There are 300 monthly origins, January 2000 to December 2024. Targets end in June 2025. These are not ONI three-month means or official ENSO event labels.

Warm water volume is the volume above 20 C between 5 S and 5 N. Basin bounds are 120 E to 80 W. Western bounds are 120 E to 155 W. GODAS combines an ocean model with observations. Its indices are not direct measures of all ocean heat. Volume anomalies use 1981-2010 means and are divided by 10^14 cubic metres. Temperature anomalies use 1991-2020 means, in C. The fixed bases are part of the revised data products. We assume that current-month inputs are available; actual release delays and historical data versions are not tested.

Exact files used in place are:

- ./datasets/noaa-pmel-godas-wwv-basin-20261109/wwv.dat; SHA-256 857fc7d0cc2bd388f1d33eb47993e8d0247914f2ca75c6b2944b880c9968afc0; 19808 bytes.
- ./datasets/noaa-pmel-godas-wwv-west-20261109/wwv_west.dat; SHA-256 5522e225a610095c9e3754668b2f7ef01aaa08d90c3fbc45e623b93cd285d9a9; 19809 bytes.
- ./datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt; SHA-256 bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012; 67087 bytes.

files/results/provenance.json records source URLs, snapshot date, absolute shared paths and resolved paths. Source records and month-level derivatives remain outside the package. The hashes define the data versions.

## Method

Let T be current Nino 3.4 temperature, V basin volume, W western volume, and s and c the sine and cosine of 2*pi*(month-1)/12. The primary mean model uses ordinary least squares to predict T at t+6 from ten columns: 1, T, V, T-T(t-3), s, c, T*s, T*c, V*s and V*c. Training starts in April 1980. One fit at the start of each origin year uses only rows whose target year is less than that year. The fit stays fixed through the year. Current monthly predictors still change. For example, a 2000 fit can use targets through December 1999 but no target in 2000.

Earlier forecasts from origins in 1990-1999 supply initial error calibration. Each variance fit uses only errors whose target year is less than the issue year. These errors come from earlier-only mean forecasts, not residuals from a full-data fit. The first variance fit uses 114 errors. This separates fit errors from test errors and prevents use of unavailable targets. The mean is identical across each variance comparison.

The reference has log(error variance) = b0+b1*s+b2*c+b3*T. The main alternative adds b4*W. A secondary check adds b4*abs(W) instead. These use four and five coefficients. The signed term tests a direction, and the absolute term tests amplitude. A Gaussian likelihood estimates coefficients without a penalty, floor, cap or score tuning. Analytic gradients and Hessians enter a trust-region solver. All fits have maximum absolute gradient below 10^-7. Variance estimates measure squared error about the forecast. They can include mean bias as well as physical noise.

The main score is Gaussian negative log density, 0.5*[log(2*pi*v)+e^2/v], where e is the forecast error and v its predicted variance. Units are nats for numerical temperature in C. Positive reference-minus-test gain favors the test. Secondary measures are coverage and width of a 90% normal interval, and interval score. The interval half-width is 1.64485362695*sqrt(v). Interval score is full width plus 20 times the distance of a target outside the interval. Smaller density and interval scores are better. Near-90% total coverage alone does not prove conditional calibration.

We average paired monthly scores by origin year. Circular blocks of three years give 10,000 bootstrap draws with seed 288628. Five-year blocks are a planned sensitivity check. All years have 12 forecasts. Percentile limits give conditional 95% intervals. The bootstrap resamples the fixed score series; it does not repeat fits. It assumes enough stability of that series. It omits source, model-choice and fit uncertainty beyond that expressed in the saved losses. Short blocks may not capture all dependence from ENSO cycles, overlapping forecast windows and expanding fits. We claim no simultaneous coverage across checks.

A planned mean-model check adds W, W*s and W*c to the mean predictors. We repeat all earlier forecasts and variance fits for it. This tests whether the main conclusion depends on leaving western volume out of the mean. The early and late subsets, 2000-2011 and 2012-2024, are descriptive checks. We do not select a favorable model or time boundary.

## Results

| Mean model | Variance rule | Mean density score | 90% coverage | Mean width, C | Interval score, C |
|---|---|---:|---:|---:|---:|
| basin_mean | ref | 0.94680 | 89.00% | 2.0899 | 2.6100 |
| basin_mean | signed | 0.95245 | 88.33% | 2.1258 | 2.6243 |
| basin_mean | absolute | 0.94780 | 89.00% | 2.0955 | 2.6113 |
| west_mean | ref | 0.98270 | 88.67% | 2.1304 | 2.6797 |
| west_mean | signed | 0.98905 | 89.00% | 2.2074 | 2.6866 |
| west_mean | absolute | 0.98772 | 88.33% | 2.1288 | 2.6978 |

The reference contains season and signed temperature. The signed and absolute rules add western volume to that reference. The west_mean setting also includes western volume in the mean model.

| Mean model | Added variance term | Mean gain, nats | Three-year block limits | Five-year block limits |
|---|---|---:|---|---|
| basin_mean | signed | -0.00564 | -0.01254 to +0.00022 | -0.01376 to +0.00023 |
| basin_mean | absolute | -0.00100 | -0.01450 to +0.01420 | -0.01339 to +0.01416 |
| west_mean | signed | -0.00634 | -0.02349 to +0.00611 | -0.02216 to +0.00610 |
| west_mean | absolute | -0.00502 | -0.00733 to -0.00272 | -0.00688 to -0.00332 |

Both signed-volume comparisons have intervals across zero. The primary three-year upper limit is only slightly above zero, but the interval is conditional on the selected method. It does not give a universal bound on possible forecast gain. The main signed-term gain was -0.00892 nats in 2000-2011 and -0.00262 in 2012-2024. Thus the two fixed subsets have the same point direction.

The absolute-volume rule gave no clear gain with the main mean model. It had worse density scores with the larger mean model, with both block intervals below zero. This is a secondary finding, not evidence that larger heat content causes worse predictability. Full subset values, all variance coefficients, 150 fit checks, annual scores and bootstrap draws are in files/results/. Every main and secondary full-period point estimate favored the reference variance rule.

## Meaning and limits

This test did not support a useful added signed western-volume variance term beyond season and temperature. It gives a negative benchmark for one forecast method and lead time. It does not reject the mechanisms in prior ensemble experiments. Model spread and realized statistical forecast error are different quantities. Omitted wind events, nonlinear responses, bias and model error can affect the result.

Only 25 test years and a small number of ENSO cycles support the inference. The record starts in 1980. Gaussian forecast distributions, fixed anomaly bases, revised products, one lead time, chosen calibration period and linear variance predictors limit the test. We did not test operational ensembles, real-time data, other variance functions or water-system impacts. The normal intervals can miss skew and extremes. No causal effect or equality of physical noise is established.

## Reproduction and checks

The analysis checks input hashes and a complete monthly sequence. A separate audit parses all three source files without the analysis parser. It uses a pivoted QR least-squares solver to rebuild earlier-only mean forecasts, checks each variance-fit gradient, recomputes density scores with scalar formulas and rebuilds annual mean density scores. The largest mean difference was 5.22e-15 C; the largest density difference was 1.96e-14 nats. The largest audited variance gradient was 1.21e-9. These checks passed. They validate arithmetic, not the physical explanation. The reference primary density score also agrees with the prior temperature-variance publication to five decimal places.

After SCI verification, extract the bundle. Use the three shared files above in place, or run `python files/retrieve.py /absolute/external-inputs`. Retrieval checks frozen hashes and refuses revised web files. Exact old bytes may no longer be available from current URLs. The frozen shared files or another copy with matching hashes are then required. The raw bytes are not bundled. This is a limit on long-term reproduction, not an unrecorded source.

From the extracted publication root, run:

```sh
python files/analyze.py --data-root /absolute/external-inputs --out /absolute/repeat-results --scratch /absolute/repeat-monthly
python files/audit.py --data-root /absolute/external-inputs --results /absolute/repeat-results --scratch /absolute/repeat-monthly
```

For shared-data reproduction, use the absolute path to the campaign datasets link as data-root. Outputs must remain outside the signed publication. Python 3.12, NumPy, pandas, SciPy and Matplotlib suffice. files/results/environment.json gives exact analysis versions. Code, aggregate scores, fits, bootstrap draws, figure, notices and hashes are preserved. No private workspace is needed except as an optional source of the frozen external bytes.

## Rights and job record

We thank GTMBA Project Office, NOAA/PMEL, NOAA/NCEP and NOAA Climate Prediction Center. No NOAA endorsement is implied. These are research forecasts, not official forecasts. We do not claim ownership of NOAA data. Only original code, narrative, figures and aggregate analysis output are included under the unchanged SCI baseline license. External source credit and terms are identified in files/EXTERNAL_DATA.txt. Source rows, derivative monthly databases and paper content are excluded.

Job: sci-1107-dell-earth-and-ocean-sciences-288628d7e6b8. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. No other agents were used. The campaign-machine signing key is not a personal authorship claim. Private keys are outside this package.
