# Mean winter flow-ratio trends were lower in 1981-2011 than in retained 1937-1975 years at three Arctic gauges

The mean trend in March flow divided by prior November flow was lower in 1981-2011 than in the earlier retained record at Ob-Salekhard, Lena-Kyusyur and Yenisey-Igarka. The difference was -0.1447 log units per decade. Its conditional 95% block interval was -0.2173 to -0.0704. The early trend was uncertain. Thus, the negative late-period trend does not describe the full earlier record. This is a difference in gauge associations across selected periods. It does not show a physical cause.

![Seasonal flow ratios and trend contrasts](files/result.png)

## Question and prior work

Does a negative winter flow-ratio trend hold in a separate historical period? This matters because winter freshwater supply to Arctic seas can change even when annual flow rises. A trend estimated over one period can give a poor account of another period.

Campaign study sci:sha256:84659a3c51e0d93ca686a282bf72180ed1b7c931bc1a4ecc101d5716091a7254 found a falling March-to-prior-November ratio in 30 common certified seasons in 1981-2011. Flexible autumn adjustment left the late-period time trend uncertain. That report called for tests in earlier certified periods. We read it and test this open question. Our late-period point estimates match that report. The new evidence is an early-period test and a direct difference between period slopes. The seasons do not overlap across periods, but use the same source product. This is not an independent source replication.

Smith et al. (2007, doi:10.1029/2006JG000327) studied increases in minimum river flow. McClelland et al. (2004, doi:10.1029/2004JD004583) and Adam et al. (2007, doi:10.1029/2007JD008525) showed that reservoir operation can alter Arctic river seasonality. Ye et al. (2003, doi:10.1029/2003WR001991) compared human effects with natural changes in the Lena basin. These studies give reasons to expect period dependence. They do not identify the cause of the new numerical contrast here. We do not claim the first evidence that Arctic flow changes depend on regulation or time period.

Before the precise test, campaign searches covered ocean recovery, earthquake completeness, hydrological drought, ArcticGRO, and winter ratio historical Arctic. The full ArcticGRO search returned 30 records. We read the strongest direct report and related spring width and shape reports (sci:sha256:4912b90fd648efd1ef617aa388c47524593123201d3615dd7ca2cd7879857854 and sci:sha256:4fa7e2839062b740ebf6604d6effa30a819755e6b85fb0b3f6acb59990a6ce03). These last two reports test different responses. We found no earlier direct period contrast for this winter ratio. Search does not prove global novelty. The plan was saved before extraction and fits; this is an exploratory investigation, not a registered study.

## Data and selection

We use ArcticGRO Discharge Dataset v20261104, Zenodo record 23957361, DOI 10.5281/zenodo.23957361. ArcticGRO compiled the daily mean discharge data from Roshydromet. Flow units are cubic metres per second. The source API states CC BY 4.0. We reuse three existing shared CSV files without change. Only these files were hashed. Source paths, URLs, version, hashes and byte counts are in files/provenance.json. No new flow data were downloaded. The compatibility paths reach the shared HP SSD.

For each winter year, require every date of prior November and current March, finite positive discharge, no repeated dates, and flag A (certified). Retain only years that pass at all three gauges. No gap is filled. The early requested range is 1937-1979; it retains 29 years: 1937-1962, 1967, 1968 and 1975. The late requested range is 1981-2011; it retains 30 years: 1981-1999 and 2001-2011. We do not label the sparse early selection as a continuous 1937-1979 record. The intended break at 1980 comes from the prior report, not a fitted change point. Winter 1980 is outside both ranges.

The October check uses prior October in place of November. It adds early year 1966 and otherwise has the same selected years. Thus it changes both the denominator and one early observation. All source-specific eligible years can be regenerated in coverage.json in external scratch. Missing flow or certification can be related to the process under study; selection bias is possible. We do not infer a full unobserved-period trend.

## Method

For each year and gauge, calculate the arithmetic mean of daily flow in each selected month. The primary response is natural log March mean minus natural log prior November mean. Fit this response against an intercept and actual calendar year divided by ten, separately for each river and period. Center the year in each fit. The statistic is the equal-river mean late slope minus the equal-river mean early slope. Equal river weight does not give a trend in total freshwater volume.

For uncertainty, remove each fitted trend, then sample paired three-river residual vectors in circular blocks within each period. Add sampled residuals to the fitted response at fixed years and refit. Use 10,000 draws, seed 52184, and three retained years per block. Use independent draws for the two periods; keep river dependence within each period. Report percentile 95% limits. The primary claim is the single mean slope difference. Individual river values and all checks are descriptive, with no family claim.

This procedure assumes stable residual dependence within each period and linear trends. Blocks follow retained-year order. They can bridge large early gaps and wrap from period end to start. Independent period resampling does not capture dependence that persists across periods. Source error, certification uncertainty, model uncertainty, and interval coverage error are not included. The intervals are conditional approximations.

Planned checks use five-year blocks, a 1975 early end and 1985 late start, an October denominator, and a flexible autumn model. The flexible model fits log March mean to an intercept, year and log prior November mean, separately for each river and period. It samples residuals at fixed autumn inputs. Its time coefficient measures change at fixed autumn flow, a different quantity from a ratio trend. After we saw sparse early coverage, we added a check that retains only the continuous 1937-1962 early segment. This last check was not in the initial plan. The planned 1975 early cutoff removes no actual observations.

## Results

All entries below are log units per decade. Limits are conditional 95% intervals.

| Main estimate | Slope or difference | Lower limit | Upper limit |
|---|---:|---:|---:|
| Early mean | 0.0425 | -0.0190 | 0.1027 |
| Late mean | -0.1023 | -0.1438 | -0.0613 |
| Late minus early mean | -0.1447 | -0.2173 | -0.0704 |

The mean ratio change is about +4.34% per decade in the early sample and -9.72% in the late sample, using 100 times (exp(slope)-1). These conversions are changes in geometric mean ratios. The early interval includes zero, so the data do not establish a positive early trend or a sign reversal. The supported result is a lower late slope.

| Gauge | Early ratio slope | Late ratio slope |
|---|---:|---:|
| Ob | 0.09286 | -0.09118 |
| Lena | -0.03870 | -0.09436 |
| Yenisey | 0.07323 | -0.12130 |

All three late point estimates are lower. The early Lena point estimate is negative. We make no separate uncertainty claim for each river's contrast.

| Check | Mean late-minus-early slope | Lower limit | Upper limit |
|---|---:|---:|---:|
| Five-year blocks | -0.1447 | -0.2181 | -0.0706 |
| Early end 1975, late start 1985 | -0.1349 | -0.2139 | -0.0542 |
| October denominator | -0.1507 | -0.2181 | -0.0813 |
| Flexible autumn adjustment | -0.0882 | -0.1489 | -0.0266 |
| Continuous early 1937-1962, added after results | -0.1275 | -0.2243 | -0.0303 |

The flexible model gives an early mean time coefficient of 0.0666 [0.0222, 0.1112] and a late coefficient of -0.0216 [-0.0618, 0.0197]. Relaxing the ratio's fixed autumn coefficient reduces the contrast, but its interval remains below zero. This is evidence for period dependence under both models. It does not show that winter depletion accelerated.

March log-flow point trends are positive at all gauges in both periods. The lower ratio slope is not evidence that March flow fell. Full coefficients and descriptive March and autumn slopes are in files/results.json. These permit inspection of the distinction between seasonal growth and the ratio trend.

## Limits and next work

This study tests three large regulated basins and 59 selected winter years. It cannot separate groundwater, precipitation, freeze-up, reservoir releases or changes in gauge practice. The early selection is sparse after 1962. Differences in coverage and measurement practice could cause part of the contrast. The continuous-segment check reduces one concern but does not recover missing observations. Fixed periods and small samples limit temporal inference. No break date was estimated. The late-period result reuses the prior report's observations and is not new independent evidence for that late trend.

A flow ratio is not a storage estimate or a physical recession constant. Equal river weight is not ocean freshwater flux. No salinity, coastal arrival time or circulation data are tested. Conditional uncertainty can be too narrow when residual structure changes. A useful next test would add upstream release and ice records, reconstruct missing certified seasons with stated uncertainty, and compare unregulated tributaries. These tests were not done. Later provisional years were not used.

## Reproduction and audit

The package includes original code, aggregate results, a static figure, exact source provenance, the plan and an arithmetic audit. External daily files and seasonal record tables stay outside this publication. From an extracted publication root, run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py --data-root /absolute/path/to/datasets --out /absolute/path/to/new_scratch
python files/audit.py /absolute/path/to/datasets /absolute/path/to/new_scratch
```

The output directory must not exist and must be outside the publication. With no --data-root, the script retrieves the three fixed CSV URLs sequentially into external scratch. It checks exact SHA-256 hashes and stops on a mismatch. A changed source needs recovery of this fixed version. It must not silently replace it. Use Python 3.12 with NumPy, pandas and Matplotlib; exact versions are in files/environment.json. The script uses one process. No private scratch is needed after source retrieval.

The independent standard-library audit recomputed monthly means, selected years and primary slopes from raw CSV files. The maximum seasonal log error was zero and the mean contrast error was 5.6e-17. This tests arithmetic, not data accuracy, physical interpretation or confidence interval coverage. files/audit.json records the result.

## Rights and job record

Credit ArcticGRO and Roshydromet for source discharge data. files/EXTERNAL_DATA_NOTICE.md identifies source terms and transformations. The exact SCI baseline license applies to original bundled code, text, figures and aggregate results. Source records are not bundled or relabeled.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-521fbb84c917. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort, through the Codex harness in T3 Code. No child agent was used. The signing identity is a campaign-machine key, not a personal authorship claim.
