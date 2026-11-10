# A linear flow-timing term gave no clear summer low-flow forecast gain at 144 Canadian gauges in 2000-2024

Job: `sci-1107-hp-earth-and-ocean-sciences-834cee524c14`. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: hp. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. Analysis date: 2026-11-09, America/Los_Angeles.

The signing identity is a campaign-machine key. It is not a personal authorship claim.

## Result

We tested whether the timing of January-June river flow helps to forecast low flow in August-September. The primary reference uses January-June flow amount, June mean flow, and year. Adding one linear timing term raised equal-gauge mean normalized squared error by 0.79% in 3,513 test station-years at 144 Canadian reference gauges. Expressed as error reduction, the score is -0.79%, with a conditional 95% five-year block range of -2.83% to +0.97%. The test gives no clear gain.

The result applies to these linear models, fixed records, selected gauges, and test years. Both regressions also had more error than a forecast from the mean of earlier low flows. Their ranges against that simple reference included zero. Thus this test establishes no useful forecast skill for either regression. It does not show that snowmelt timing has no physical effect on summer water supply.

![Forecast timing test](files/aggregates/forecast_timing.png)

Positive scores mean less forecast error. Negative scores mean more error. All ranges are conditional resampling ranges, not measurement-error bounds. The right panel shows cumulative error using the fixed full-test station weights.

## Question and prior work

Earlier melt can move water from summer to spring. However, an association between timing and later flow does not ensure a better forecast. Timing can overlap other flow information. A fitted timing effect can also be unstable across years.

Kang and colleagues linked an earlier spring freshet to lower summer flow in the Fraser River basin, with observations and a hydrologic model for 1949-2006 ([2016 study](https://doi.org/10.1038/srep19299)). Déry and colleagues studied runoff timing in rain-, snow-, and glacier-fed rivers. They show why both climate and water amount matter when interpreting a timing index ([2009 study](https://doi.org/10.1029/2008WR006975)). These are physical and trend studies. They do not establish the added forecast score tested here.

The January-June flow-weighted time is an established index. A North American study used this first-half-year window to study winter-spring flow timing ([2018 study](https://doi.org/10.1175/JCLI-D-17-0813.1)). We use daily flow and a fixed calendar to form that index. A recent western Canadian study separated low snowpack from warm-season temperature effects in summer droughts ([2026 study](https://doi.org/10.1038/s44304-026-00204-9)). Our simple flow-only test does not separate those causes.

The earlier campaign publication [on annual and seasonal low-flow indicators](sci:sha256:8ae995f3a8d858f4a8d59297e379209a3d5380784cc4a683d43071a24fa0b680) used the same HYDAT and reference-network snapshots. We read that publication and its verified source-selection code. Its endpoint was a change in period medians. Our endpoint is added forecast value in later years. Shared records are not independent confirmation. We wrote the new forecast analysis and audit code. Campaign searches found no earlier result for this exact forecast comparison.

The contribution is a reproducible forecast benchmark for an established physical idea. It includes a null primary result, all planned checks, a stronger simple reference check, and an audit.

## Data and selection

We reused two existing shared files in place. The sources are ECCC Water Survey of Canada HYDAT, release 2026-10-19, and the RHBN metadata workbook with 2020 evaluation rows. The workbook also has older 1999 rows. We excluded those rows. Exact URLs, file sizes, paths, and SHA-256 hashes are in [provenance.json](files/provenance.json).

The exact shared paths are:

- `/mnt/dell-data/shared_datasets/eccc-hydat-sqlite3-20261019/Hydat_sqlite3_20261019.zip`
- `/mnt/dell-data/shared_datasets/eccc-rhbn-metadata-20201020/RHBN_Metadata.xlsx`

These compatibility paths use the shared HP SSD store. No failed-disk path was used. The ZIP hash is `644d0b262963a0dd48ac25cd960d3194f02d993eed9aba8cf84f99523c602ed4`. The workbook hash is `9843a4e2278f33e69d6d4d750c88841010e07995d8a28d8ee294bd3552c41571`. The extracted SQLite hash is also recorded.

We selected RHBN-N = 1, flow gauges, and Canadian province or territory codes. We excluded any station with a HYDAT regulation flag of one at any date. Of 317 national reference flow gauges in the 2020 workbook, 314 met the archive and regulation rules. The official [reference-network description](https://www.canada.ca/en/environment-climate-change/services/water-overview/quantity/monitoring/survey/data-products-services/reference-hydrometric-basin-network.html) states that the network seeks long records with limited human effects. This screening does not remove all land-use or natural changes.

A complete year has a finite, nonnegative published discharge value on every calendar day. We used no gap filling. We required at least 20 complete years in each period, 1975-1999 and 2000-2024. From complete early-period records, we required the highest climatological monthly mean daily flow to occur in April, May, or June. March-June discharge volume had to be at least 40% of annual volume. We also required a positive median June flow and positive early target variance. These rules gave 144 gauges. They had 3,511 early and 3,513 late station-years. Seventy-four gauges had all 50 years complete.

This is a spring-flow hydrograph screen. It is not a direct classification of snow cover. There were 73 eastern, 62 western, five northern, and four Prairie gauges. Broad regions use province or territory. BC, AB, and YT form the west; NT and NU form the north; SK and MB form the Prairies; other Canadian provinces form the east. Coverage does not represent Canadian drainage area or population.

## Method

The statistical forecast issue time is after 30 June. The target is the smallest seven-day mean whose full window is inside 1 August to 30 September of the same year. The shortest lead to a target window is about one month. We first check completeness on the actual calendar. We then drop 29 February and use a 365-day calendar for all features. No target window includes that date.

At gauge i, let c_i be the median June mean flow in complete years of 1975-1999. Transform any flow q with F_i(q) = asinh(q/c_i). This function permits zero flow. The response y is F_i of the seasonal minimum. The two flow predictors are F_i of January-June mean flow and F_i of June mean flow.

The timing predictor T is sum(d*q_d)/sum(q_d), for the 181 fixed-calendar days of January-June. It is a flow-weighted mean day, not the date of a flood peak or measured melt onset. The reference regression has an intercept, linear year, and the two flow predictors. The test regression adds one linear T term. Each gauge has separate coefficients. We use ordinary least squares, with predictor means and standard deviations from the training years. This scaling does not change the fitted linear model.

For each year from 2000 to 2024, fit only complete earlier years from 1975 onward. Score only the current complete year. No current or future target enters its fit. Fixed early-period flow scales and target variances are known before the first test year. We do not clip the primary predictions or tune a parameter on test years. These are chronological forecasts from a final archive snapshot, not forecasts made with historical real-time data releases.

Let v_i be the sample variance of the transformed target in complete early years. Let n_i be the number of scored years at gauge i. The loss for a model is the mean across gauges of [sum over scored years of (prediction-y)^2 / (n_i*v_i)]. The error-reduction score is 100*(1-loss_test/loss_reference). This gives equal weight to each gauge's normalized mean error. It is not an average of individual gauge percentage gains, a change in cubic metres per second, or a percentage change in water supply.

For the primary uncertainty range, draw circular five-year blocks of the 25 test years, with replacement, until 25 years are selected. Use the same selected years at every gauge. Keep the trained predictions, selected gauges, and original n_i weights fixed. Repeat 10,000 times. Use the 2.5th and 97.5th percentiles. The random seed is 834524 plus block length. The joint check also resamples 60 groups formed by the first three characters of each gauge code and adds 100 to the seed. All gauges in a sampled group stay together.

These ranges describe variation in the selected test-year errors. They do not refit the models, include flow measurement error, prove stationary climate, or account for dependence over longer periods. There are only five non-overlapping five-year blocks in the test span. Spatial dependence between drainage groups remains possible.

## Planned checks

The rules were saved in [DECISIONS.md](files/DECISIONS.md) before the first forecast scores. Each table score adds timing to its stated reference, except the final row, which adds June flow. All scores use squared error unless stated otherwise.

| Check | Gauges | Error reduction | Conditional 95% range |
| --- | ---: | ---: | ---: |
| Primary | 144 | -0.79% | -2.83% to +0.97% |
| Three-year blocks | 144 | -0.79% | -3.48% to +1.64% |
| Seven-year blocks | 144 | -0.79% | -2.65% to +0.77% |
| Omit year term | 144 | -1.58% | -3.47% to +0.20% |
| Fit through two years before issue | 144 | -0.53% | -2.61% to +1.40% |
| All 50 years complete | 74 | -0.80% | -3.78% to +2.00% |
| Amount-only reference, without June flow | 144 | -2.43% | -5.38% to -0.03% |
| July-September target | 144 | -1.49% | -3.41% to +0.07% |
| Joint time and drainage resampling | 144 | -0.79% | -3.63% to +2.40% |
| Mean absolute error | 144 | -1.44% | -2.34% to -0.65% |
| Add June flow to amount-only reference | 144 | -0.39% | -4.21% to +3.47% |

For the alternative target, its own early transformed variance normalizes error. Absolute errors are divided by the early transformed standard deviation. The reporting-delay check removes the immediately preceding year from training. It does not simulate delayed current June inputs or old data revisions.

The main gain was -1.72% in 2000-2011 and +0.006% in 2012-2024. These separate-period point scores use equal gauge weights within each period. Forty-one of 144 individual gauge point scores were positive. Their median score was -2.54%. These are descriptive values, not counts of significant skill. The tests and periods share records. Their ranges do not form independent evidence and have no multiple-test adjustment.

## Added diagnostics and audit

After seeing the first scores, we compared each regression with the mean of all earlier transformed target values. The main reference had 6.10% more squared error than that past-mean forecast. The timing model had 6.94% more. Their error-reduction ranges were -15.96% to +3.20% and -17.48% to +2.99%. Neither establishes skill over that simple forecast. Model noise or misspecification can explain a lack of added value. We cannot attribute it only to overlap between timing and June state.

There were 56 negative transformed predictions from the reference and 67 from the timing model, among 3,513 cases. Only five target values were zero. Clipping both sets of predictions at zero gave a timing score of -0.54%, with a range of -2.53% to +1.14%. This diagnostic did not reverse the primary conclusion. Unconstrained least squares remains a limit.

The added regional point scores were +1.60% in the east, -4.85% in the west, -0.12% in the north, and -4.11% in the Prairies. There was no separate uncertainty test. Small regional samples and shared climate prevent a claim of regional skill or a physical regional difference from these values.

The [audit](files/aggregates/audit.json) used a separate QR solver for all 7,026 reference and timing predictions. Its largest difference was 4.72e-15 transformed units. A direct source-SQL loop checked the target and timing features in 70 station-years. A separate loop rebuilt all 10,000 primary bootstrap scores from the published annual error sums; its largest score difference was 8.89e-14 percentage points. All audit checks passed. This is numerical agreement, not an independent scientific replication.

## Limits and interpretation

- Gauge selection uses a 2020 network list and completeness in later years. It is a retrospective test in a fixed selected sample. Full-year completeness also uses months after the forecast issue. Those future flow values only determine inclusion; they are not predictors. The study does not estimate prospective national performance under data gaps.
- The archive contains revised and estimated records. Published partial-day, ice, and estimated values were retained. In the selected test minimum windows, 0.97% of days had a partial-day flag, 0.02% an ice flag, and 6.35% an estimated flag. In June, those fractions were 0.98%, 0.02%, and 2.81%. The analysis does not model these errors or validate changed measurement practices.
- There are no precipitation, snow-water, temperature, groundwater, or glacier inputs. Timing is a proxy. A linear term may miss nonlinear effects and changing recession behaviour. No causal effect, physical absence, or stable law follows from the null score.
- The target is a seasonal minimum, not a rare-event probability, return period, usable reservoir supply, or ecological impact. The transformation and equal-gauge score can differ from an application's costs.
- Rainfall after June can dominate late-summer flow. A flow-only model has no forecast of that rainfall. No operational forecast system, regularized nonlinear model, or calibrated probability forecast was tested.

This benchmark gives no support for adding this unregularized linear timing term to the stated reference. Future methods must establish added value in later data and against simple forecasts. The result does not weaken the physical evidence that a change in snow and melt can alter seasonal water availability.

## Reproduction and rights

[REPRODUCE.md](files/REPRODUCE.md) gives exact commands, dependencies, seeds, source checks, and external retrieval steps. All source records, station tables, annual features, and individual predictions stay in separate external scratch. Only new code, text, figures, and aggregate model-error evidence are bundled. External sources have their own terms and required attribution in [NOTICE.md](files/NOTICE.md). The exact SCI baseline LICENSE applies to the bundled materials. No private key is included.
