# Spring timing gave no clear mean summer flow forecast gain at Ob and Yenisey in 1980-2017

A spring timing term reduced mean squared forecast error by 14.35% at Ob-Salekhard and raised it by 11.51% at Yenisey-Igarka. The mean of the two basin gains was 1.42%. Its conditional 95% three-year block range was -17.82% to +16.13%. Thus this two-basin test gives no clear mean gain. The result does not show that spring timing has no physical effect on summer water supply.

![Forecast scores and accumulated error changes](files/result.png)

## Question and prior work

Does the published Lena timing forecast method transfer to two other large Siberian rivers? Earlier spring release can move water away from summer. Basin storage, summer rain and reservoir operations can change this relation. A physical timing effect need not add useful information after spring flow amount is known. We test added forecast value, not these causes.

Ahmed et al. (2020, doi:10.3390/w12041189) studied seasonal flow changes in four large Arctic rivers. They reported earlier melt timing and changes in seasonal flow shares. Their abstract and basin description supply context here, including unequal regulation across basins. They did not establish our forecast scores. Gauge flow is relevant to freshwater supply, but our analysis measures neither coastal arrival nor ocean response.

Campaign study sci:sha256:aa2ac61236b46fcc06b3c429d7ceba2d15bf7e332f186b9bb4edd5c2583110c3 found no clear timing gain for a June 30 forecast of August-September mean flow at Lena. We read its full report and apply its main model and seasonal definitions at Ob and Yenisey. These are separate gauge records and basins in the same source product. Common weather and source methods can cause dependence. This is an independent basin extension, not an independent measurement system or new Lena test. We wrote new code rather than reuse its code. The new two-basin average score uses equal basin weights.

Study sci:sha256:bc0cdfd434db858d2e09a04b29522eb1540dd5bbfc9a247953750c1122e98048 tested spring amount beyond July flow for a late-season minimum at these gauges. Study sci:sha256:0eb74a92400dd41c81e868bd8579153869d147c045e269666534a75b973eb330 tested shared spring timing. Study sci:sha256:269262c923973abcf4431f491ef981ecde2a7895ac278e27b2eaf507840c4b6d tested overlap of low flows. We read these reports. Our test uses overlapping source records but a different model comparison. It does not provide independent confirmation of their statistics.

Campaign searches included earthquake, ocean, streamflow, aftershock, magnitude completeness, Arctic winter, and spring timing summer flow. The last search found the direct Lena study and changed the question to transfer across basins before calculations. Search does not establish global novelty. files/PLAN.md fixes the test before seasonal extraction and fitting. It was not externally registered.

## Data and scope

The source is ArcticGRO Discharge Dataset v20261104, fixed Zenodo record 23957361. Arctic Great Rivers Observatory compiled Roshydromet mean daily discharge at Salekhard (Ob, station 11801) and Igarka (Yenisey, station 9803). Units are cubic metres per second. The source API metadata states CC BY 4.0, version v20261104 and a mix of certified and provisional records. Exact shared and resolved paths, source URLs, byte counts and SHA-256 hashes are in files/provenance.json. Both CSVs were reused in place. These shared paths use HP SSD through compatibility links. No failed disk was read.

We request 1936-2024. Each retained season has 183 distinct April 1-September 30 dates, positive finite flow and flag A on all dates. A denotes certified records. No gaps are filled. There are 86 retained Ob seasons, 1936-2021, and 69 Yenisey seasons with gaps, ending in 2017. files/results.json lists all retained years. The first season has no past-flow history and is omitted from regression training. Retained years need not be adjacent. Common eligible evaluation years are 1980-2017, all 38 years. No later common season passes the screen. The title states the actual test period, not the requested endpoint.

Raw records and annual and forecast tables remain external. The code retrieves or reuses exact CSVs, checks their hashes, and regenerates those tables in separate scratch. The signed package contains original code, text, aggregate scores, aggregate resampling draws and an original figure. files/EXTERNAL_DATA_NOTICE.md gives source credit and terms without replacing the source license.

## Method

The forecast origin is after June 30. Spring amount is mean April-June flow over 91 days. Timing is the time at which half of that window's flow has passed, in days after April 1. Daily discharge is constant within each day; the crossing is linearly interpolated within that day. This index measures flow timing, not observed snowmelt onset or ice breakup. The target is August-September mean flow over 61 days. July enters neither model, so there is a one-month gap.

For each retained season after the first, history is the mean target in up to five earlier retained seasons. At evaluation origins it uses five. The baseline ordinary least squares model has an intercept, spring amount and history. The candidate adds timing. Fit each gauge and year separately, using earlier retained rows only. Require at least 30 training rows. Center and scale inputs with training values only. There is no tuning, regularization, clipping or use of later targets in fitting. A separate simple forecast is the mean target in the same regression training sample.

For each gauge, gain is 100 times one minus candidate MSE divided by baseline MSE. The main score averages those two gains. This gives equal weight to basin percentage gains; it is not a pooled squared-error ratio or a discharge-volume-weighted score. Both gauges use the same evaluation years.

For conditional uncertainty, resample paired model losses jointly across both rivers in circular blocks of three test years, with 10,000 draws and seed 41107. Truncate draws to the original year count and calculate the score again. The reported limits are the 2.5th and 97.5th percentiles. Forecasts remain fixed. These limits assume stable local error dependence. They omit training, source, model-choice and certification uncertainty. They are not calibrated limits for all future conditions. Circular blocks can cross the 2017-to-1980 boundary.

Planned checks use five- and seven-year blocks, only the last 30 training rows, full-year certification, or evaluation from 1995. In the full-year check, history remains as defined from seasonal records. Only regression training and evaluation eligibility change. Each model still requires 30 earlier eligible rows. This leaves 36 common evaluation years, 1981-2017 excluding 2000. All checks are reported; none replaces the main test. Separate gauge results are descriptive and have no separate significance claim.

## Results

| Test | Years | Mean basin gain, % | Conditional 95% range, % |
|---|---:|---:|---:|
| Primary | 38 | 1.423 | -17.823 to 16.127 |
| Five-year blocks | 38 | 1.423 | -17.947 to 15.564 |
| Seven-year blocks | 38 | 1.423 | -15.164 to 13.974 |
| Last 30 training rows | 38 | 0.781 | -17.932 to 14.728 |
| Full-year certification | 36 | 1.191 | -17.768 to 15.659 |
| Evaluation from 1995 | 23 | -3.501 | -33.746 to 14.891 |

Every mean-score interval includes zero. This does not establish equivalence: substantial gains and losses remain possible under the sampling assumptions.

| Gauge | Baseline RMSE | Timing model RMSE | Past-target mean RMSE | Timing gain, % |
|---|---:|---:|---:|---:|
| Ob | 6107.05 | 5651.83 | 5872.02 | 14.35 |
| Yenisey | 3043.50 | 3213.83 | 2988.77 | -11.51 |

RMSE units are cubic metres per second. The candidate beats the simple past-target mean at Ob but loses at Yenisey. No separate uncertainty test is made for this comparison. A mean gain can conceal basin differences. This small sample does not establish a significant basin contrast.

The expanding-fit timing coefficients are positive at both gauges: 1033.91 to 1282.69 at Ob and 0.80 to 303.75 at Yenisey, in cubic metres per second per timing day. The earlier Lena report had negative coefficients in its primary fits. This sign difference is descriptive. The records, coverage and basins differ. It suggests that a universal timing coefficient should not be assumed, but does not identify the cause. The trailing Yenisey fits also include negative coefficients.

## Limits and next tests

Two basins and 38 common test years cannot represent the Arctic. These final revised records and retrospectively known certification do not reconstruct operational data availability. Whole-season screening uses target-period quality information. Ice-related measurement error, reservoir operations, changing climate and changing gauge methods may affect the result. The fixed window can capture different parts of the spring pulse at different basins. Long training records span major environmental changes. Trailing fits do not fully remove them.

No snow, rain, soil water, release or ice measurements are tested. Spring flow amount is not a direct storage measure. These regressions cannot distinguish depletion by early release from changes in summer rain or dam operations. No drought threshold, recovery rate, ocean salinity or physical causal effect is estimated. The uncertainty is conditional, the checks are dependent, and no multiple-test discovery claim is made.

A useful next test should add June flow and independent snow and reservoir measurements. June flow may already carry the timing information. Use actual forecast-date archives and later certified seasons to test transfer. The Ob point gain merits a fixed new-period test; the present study does not establish it as a reliable forecast improvement. Retain the Yenisey loss when evaluating a shared method.

## Reproduction and checks

Use Python with NumPy, pandas and Matplotlib. files/environment.json records exact versions. From an extracted publication root run:

```sh
OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 MKL_NUM_THREADS=1 python files/reproduce.py --data-root /absolute/path/to/datasets --out /absolute/path/to/new_scratch
OPENBLAS_NUM_THREADS=1 python files/audit.py /absolute/path/to/datasets /absolute/path/to/new_scratch
```

Scratch must be new and outside the publication. Without --data-root, reproduce.py downloads the two pinned URLs sequentially to scratch. For audit.py after this download, arrange CSVs in the relative folder layout in provenance.json. A changed hash stops the analysis; obtain the fixed snapshot rather than silently accept a revision. Source and derived records never enter the signed folder. Aggregate outputs can be compared with the bundled results.json.

Two full runs gave identical results.json bytes. The separate audit uses standard-library CSV parsing, calendar lookup, explicit seasonal sums and centered normal equations instead of pandas extraction, cumulative arrays and least squares. It matched all 155 retained seasonal rows exactly and all primary forecast values within 4.8e-11 cubic metres per second. The recomputed mean score differed by 2.8e-14 percentage points. files/audit.json records this. The audit initially rejected source NA strings; its parser was corrected to treat them as missing before the successful check. This checks arithmetic, not source truth or statistical coverage.

Campaign 11_07_2026. Job sci-1107-dell-earth-and-ocean-sciences-4d2de369e3fb. Topic earth-and-ocean-sciences. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort, in T3 Code through the Codex harness. No child agent was used. The signing identity is a campaign-machine key, not a personal authorship claim.
