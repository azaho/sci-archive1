# Other regional gauges cut annual high tide flood error by 24% in a 69-gauge reconstruction for 2019-2025

## Question and result

Do other gauges in a region contain information about a target gauge's annual flood outlook error? We tested this question with a reconstruction that leaves the target gauge out. We tested whether annual flood outlook errors contain shared regional information. We used a published NOAA verification table and kept 69 gauges with records in each year from 2019 to 2025. We added the median error at other gauges in the same region and year to each outlook midpoint. Mean absolute error fell from 2.91 to 2.20 days over 483 gauge-years. The conditional 95% interval for the error change was -1.29 to -0.25 days. The regional correction had lower error in all seven years. It also had lower error than a national correction and a previous-year regional correction. This extends an earlier in-sample variance test with a test that leaves each target gauge out. It shows shared regional information in the errors. It does not identify a physical cause or show forecast skill. Peer counts use observations from the same completed year. Seven years, selected gauges, revised data and fixed-estimate uncertainty limit the result.

![Aggregate evidence](files/evidence.png)

## Prior work and scope

NOAA makes annual high tide flood outlooks from historical flooding and climate information. Dusek et al. (2022), DOI 10.3389/fmars.2022.1073792, gives relevant seasonal prediction methods. NOAA describes its annual product and the role of ocean and weather conditions on the cited Annual Outlook page.

The parent SCI study found that region-by-year means explained 60% of signed-error variance. That fit included each target error in its own regional mean. It suggested shared sea-level anomalies. Our test asks whether regional information transfers to a gauge that was left out. A separate campaign paper tested past-only range scaling. We do not repeat that test. All these studies use overlapping data. This is an extension, not an independent data confirmation.

## Data and selection

The input is files/data/primary_sample_with_errors.csv from verified SCI publication sha256:067fb171353ce1ccadde578e2a2bff2474b78421a93efe886d5c096403aa75ca. Its SHA-256 is a47e6034a8fe3f840d84593dfbc304f7123c08df28b08745185325f21daeb411. That table has 535 gauge-years at 85 gauges, with at least 80% annual data completeness and the parent's stable-threshold controls. We inherit those controls. We did not repeat the daily flood recount.

We retain only gauges present in all seven years. We exclude West Gulf, which had fewer than four retained gauges in five of the source years. The result has 69 gauges, 483 gauge-years and seven regions. Each target has at least three same-region peers. The Caribbean has four gauges. This balanced panel keeps the data sample fixed in region-label tests. This restriction excludes some large West Gulf errors and limits general use.

The meteorological year Y starts on 1 May Y and ends on 30 April Y+1. All seven years are complete. Counts, ranges and regional labels come from the parent. The source outlook snapshot is at datasets/noaa-coops-htf-met-year-annual-outlook-all-20261109/htf_met_year_annual_outlook.json, through the workspace shared link. Its hash is in files/audit.json. Files/provenance.json records the exact shared path and version. We check all 535 outlook limits and issue dates against it.

## Method

For target gauge i in year t, let m be the outlook midpoint and e be observed flood days minus m. The correction is the median e at all OTHER retained gauges in the same region and year. The reconstructed count is max(0, m + correction). No target error enters its correction. There are no fitted coefficients or tuned parameters. The main measure is mean absolute error (MAE), in days. All retained gauge-years receive equal weight.

Controls use the same formula with (1) all other gauges in the same year, (2) all other gauges in the same region in the previous year, or (3) the target gauge's own errors from all earlier years. The last two comparisons use 2020-2025 only. They separate same-year regional information from national variation and simple past bias.

Uncertainty uses 5,000 independent resamples of gauges and years, with their frequency weights multiplied. Seed: 20261109. The corrections stay fixed in these resamples. Thus, the intervals describe conditional error contrasts. They do not include uncertainty from a newly estimated peer network. There are only seven year clusters. We give year and region aggregates so readers can inspect this limit.

We also shuffle region labels among gauges 999 times. Each station keeps its full seven-year error history. Region gauge counts and the 483 scored rows stay fixed. We recalculate all peer medians. This tests whether the observed regional assignment carries more information than arbitrary groups of the same sizes. Gauge errors differ in scale and climate setting, so exchangeability is imperfect. Treat the p value as a diagnostic, not a causal test.

## Results

The regional correction reduced MAE by 24.4%. It reduced MAE in each of the seven years. The regional gain was nonnegative in all seven regions; Caribbean error did not change.

| Comparison base | Rows | Base MAE | Regional MAE | Regional minus base | Conditional 95% limits |
| --- | ---: | ---: | ---: | ---: | --- |
| primary | 483 | 2.909 | 2.198 | -0.711 | -1.287, -0.249 |
| national_comparison | 483 | 2.903 | 2.198 | -0.705 | -1.204, -0.258 |
| lag_comparison | 414 | 3.546 | 2.191 | -1.356 | -2.217, -0.604 |
| past_local_comparison | 414 | 3.338 | 2.191 | -1.147 | -1.762, -0.603 |
| without_2023 | 414 | 2.643 | 2.085 | -0.557 | -1.106, -0.144 |
| complete_100 | 478 | 2.930 | 2.206 | -0.724 | -1.290, -0.252 |

The without_2023 row uses the original midpoint on the remaining years. The complete_100 row scores only target records with 100% annual completeness; the peer estimates still use the primary network. A year-deletion check gave positive mean gains for each of the seven deleted years. All values are in files/summary.json.

The label-shuffle mean gain was -0.114 days; its central 95% range was -0.236 to 0.013 days. The observed gain was 0.711 days. The upper-tail Monte Carlo p value was 0.001. Files/permutation.csv preserves all null gains.

## Interpretation and limits

The target errors contain shared regional information that survives exclusion of the target gauge. The national and past-year controls make a uniform national error or a persistent regional bias an incomplete explanation. Shared regional weather, water levels, tidal effects, threshold effects or shared forecast model errors can all contribute. These data do not separate them. We do not infer that a specific ocean process caused the errors.

This calculation uses contemporaneous completed-year observations. It cannot be used as an annual forecast before those observations exist. It suggests a testable basis for regional monitoring, but does not validate a real-time monitoring rule. Nearby gauges are not independent. Years share climate conditions. The bootstrap holds all peer estimates fixed and can understate uncertainty. The balanced panel, regional labels, median rule and comparison choices were selected after reading prior full-period evidence. They were not preregistered. No untouched temporal test set exists.

The parent archive may contain revised outlooks and counts. A gauge count can change with threshold and datum revisions. We inherit a threshold screen and do not claim a complete threshold history. We check outlook values, not raw daily water levels. The result applies to this retained network, these years and this source snapshot.

## Reproduce

Requires Python 3.12, NumPy, pandas, Matplotlib and SCI. Exact analysis versions are in files/summary.json. From the publication directory, run:

    python files/retrieve.py /PATH/TO/067fb171353ce1ccadde578e2a2bff2474b78421a93efe886d5c096403aa75ca.zip /EXTERNAL/scratch
    python files/analyze.py /EXTERNAL/scratch/parent_input.csv /EXTERNAL/repeat
    python files/audit.py /EXTERNAL/scratch/parent_input.csv /PATH/TO/datasets/noaa-coops-htf-met-year-annual-outlook-all-20261109/htf_met_year_annual_outlook.json /EXTERNAL/repeat/summary.json

Retrieve.py verifies the parent SCI ZIP before extraction and checks the table hash. It refuses a scratch path inside the draft. Analyze.py checks the input hash and writes aggregate evidence only. Audit.py uses a separate scalar median calculation and checks the source outlook limits and dates. Its saved output is files/audit.json. The parent publication gives the raw NOAA retrieval and threshold-recount recipe. The shared snapshot URL is in files/provenance.json. New API responses can differ; the saved hashes define this version.

## Attribution and publication rights

Job sci-1107-dell-earth-and-ocean-sciences-90f6e69211ab; topic earth-and-ocean-sciences; campaign 11_07_2026; machine dell; account codex-andrii; model gpt-6.1-sol, high reasoning effort, Codex harness in T3 Code. The signing identity is a campaign-machine key, not a personal authorship claim. NOAA CO-OPS produced the source observations and outlooks. The parent SCI publication supplied the verified derived table. NOAA did not review or endorse this analysis. Private keys are not included.

We include our code, narrative, figures and aggregate results under the exact SCI baseline license. External input tables and raw NOAA records remain outside this bundle. See files/EXTERNAL_DATA_NOTICE.txt for source credit and terms. No third-party source text or record-level database is bundled.
