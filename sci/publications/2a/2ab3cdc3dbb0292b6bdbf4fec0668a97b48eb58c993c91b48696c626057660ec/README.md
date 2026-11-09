# Autumn DMI gave no clear added next-year ENSO forecast gain in 25 winters from 2000 to 2024

Adding autumn Indian Ocean Dipole Mode Index (DMI) gave no clear gain in this test of next-year winter Nino 3.4. Mean squared error (MSE) rose by 2.59%. The conditional 95% three-year block interval for MSE reduction was -21.83% to +17.54%. Forecast correlation rose from 0.031 to 0.258. However, a larger cold mean error offset the improvement in errors about their mean. These results apply to the stated indices, models and test winters. They do not rule out useful DMI information.

![Forecasts, error differences and model checks](files/result.png)

## Question and prior work

Can autumn Indian Ocean temperatures add long-lead information about Pacific ENSO after recent Pacific temperatures are known? ENSO affects rainfall and water supply in many regions. A useful long-lead signal could help studies of water risk. This study tests the ocean index, not local rain or water supply.

Izumo et al. (2010), doi:10.1038/ngeo760, proposed that Indian Ocean Dipole conditions help predict the next year's ENSO. Fan and Meng (2023), doi:10.1029/2023GL105525, report a stronger link for positive DMI and propose an Atlantic Ocean path. Their paper also describes the competing view that the link can arise from the ENSO cycle. We read its full public text and the 2010 public abstract. Our study does not repeat their circulation analysis or test the proposed path.

The new item is a small, open benchmark with a strict time order, saved forecasts, paired error intervals and checks for unequal slopes and baseline choice. It tests added prediction value, which a full-record correlation alone cannot establish. We do not claim to discover the IOD-ENSO link. The 25 test years overlap years in prior studies. This is a chronological model test within a known record, not a fully unseen confirmation of a hypothesis.

Campaign searches and their results are saved in files/search.json and files/search_precise.json. We read the signed text of SCI sha256:440a9a8ee47f7400dc0213b2a673313eea54c5aa75188573e973421a1c7741fe. That study tested East African rain and identified the shared index sources. We reuse those public source snapshots, not its code or forecast tables. No precise next-year ENSO test appeared in our limited search. This is not an exhaustive literature search.

## Data and provenance

We use two fixed public data files, reused in place. Neither shared file was changed. The saved monthly table contains January 1950 to December 2025. The analysis uses predictor seasons in 1950-2023 and target months through February 2025. All used seasons have three finite months. The unused late months in the table do not enter fitting or scoring.

CPC ERSSTv5 Nino 3.4 is the last anomaly column of ersst5.nino.mth.91-20.ascii. It has a 1991-2020 reference period and covers 5 S-5 N, 170 W-120 W. We use the fixed older product, not the ERSSTv6 indices now listed on the CPC index page. DMI comes from NOAA PSL HadISST1.1. It is the western Indian Ocean SST anomaly (10 S-10 N, 50-70 E) minus the eastern anomaly (10 S-0, 90-110 E). Both indices have units of degrees C. The DMI file says Created 25 July 2026 and Preliminary. Retrieval into the shared store was on 9 November 2026.

Exact shared files and SHA-256 hashes:

- ./datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt: bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012
- ./datasets/psl-hadisst-dmi-monthly-20261109-d977/dmi.had.long.data: 42c1000e221addacac4451b8b9ddfbc5ee732b99ee69b0be5105e69ebe881e05

Absolute and resolved shared paths, source URLs, byte counts and source metadata are in files/provenance.json. Only these two raw files were hashed. Full shared raw data are not copied into this bundle. The exact monthly values needed for the analysis are included.

## Method

The internal plan in files/plan.txt was written before fitting. It was not externally registered. SON means September-November. JJA means June-August. NDJ means November-January. Each season has equal month weights.

For predictor year y, the target is Nino 3.4 in November and December of y+1 and January of y+2. The seasonal midpoints are 14 months apart. We treat the forecast as issued after November of y. The target starts 11 months after December of y. Actual data release dates are not modeled.

The baseline is ordinary least squares with an intercept, SON Nino 3.4 and JJA Nino 3.4. The added model also uses SON DMI. For each origin y, training predictor years run from 1950 through y-2. The most recent training target ends in January of y, before the stated issue time. We exclude predictor year y-1 because its target is not yet complete. All centering and scaling use training rows only. The first fit has 48 rows; the last has 72 rows. There is no model tuning.

The test uses 25 origins in 1999-2023. Targets are winters starting in 2000-2024 and ending in January 2001-2025. In the title, a winter is named by its November year. The primary score is 100 times (1 - added MSE / baseline MSE). Positive values mean lower error after adding DMI.

For uncertainty, we resample paired annual squared errors in circular three-year blocks. There are 19,999 draws with seed 34582. Each draw has 25 years after trimming. The 95% interval uses the 2.5 and 97.5 percentiles. One- and five-year blocks are checks. Intervals condition on the saved forecasts. They omit model fitting, source and hypothesis selection uncertainty. A short and changing record may not meet the assumptions needed for interval coverage.

## Results

| Model | RMSE, degrees C | MAE, degrees C | Mean forecast minus target, degrees C | Correlation |
| --- | ---: | ---: | ---: | ---: |
| Earlier training target mean | 1.113 | 0.927 | -0.099 | -0.370 |
| Pacific baseline | 1.132 | 0.933 | -0.180 | 0.031 |
| Baseline plus DMI | 1.147 | 0.929 | -0.427 | 0.258 |

Both primary models have larger MSE than the earlier training target mean. Adding DMI gives -2.59% MSE reduction. The one-year interval is -22.65% to +18.02%; the five-year interval is -18.31% to +15.61%. Thus the primary result gives no clear added gain.

| Planned check | MSE reduction, % | Conditional 95% three-year interval, % |
| --- | ---: | ---: |
| Primary | -2.59 | -21.83 to 17.54 |
| Separate positive and negative DMI slopes | -5.18 | -41.48 to 17.86 |
| Absolute SON Nino term in both models | 0.26 | -10.59 to 9.08 |
| Linear time trend in both models | 12.22 | -10.71 to 32.97 |
| Last 30 training years | -4.32 | -46.22 to 30.02 |
| Omit predictor year 1997 from training | -2.82 | -21.67 to 17.51 |
| Target moved one month later to DJF | 0.68 | -18.45 to 22.03 |

These checks were not used to select a winning model. All intervals include zero. Separate DMI slopes use max(DMI,0) and min(DMI,0), with no event threshold. The absolute Nino term allows unequal warm and cold responses. The time trend changes the point gain but not the uncertainty conclusion.

The primary gain is +9.73% for the first 12 winters and -13.70% for the last 13. Removing one scored winter at a time, without refitting, gives gains from -7.54% to +1.80%. The fitted DMI slope is negative in every primary fit, from -1.231 to -0.711 degrees C per degree C. A stable slope sign does not ensure useful forecast errors.

An exploratory arithmetic check explains why correlation and MSE differ. Baseline MSE is 1.2820 degrees C squared: 1.2495 from errors about their mean and 0.0326 from squared mean error. With DMI these terms are 1.1330 and 0.1822, for MSE 1.3152. Thus the centered error falls but squared mean error rises more. This uses the test mean only as a diagnostic. It is not a bias correction available at forecast time. files/bias_diagnostic.json gives the terms. The trend check is consistent with a role for changes over time, but cannot identify their cause.

## Limits and use

The result is a null result for these simple models, not evidence that the Indian Ocean has no physical effect on ENSO. We omit ocean heat content, winds, Atlantic conditions and coupled dynamics. No physical mechanism is identified. The baseline itself has little long-lead skill. Other models, data products, target definitions or test periods may differ.

The data are revised observations. SST reconstruction, fixed reference periods and product changes limit real-time claims. No vintage data or release-time archive is used. Constant seasonal offsets are absorbed by the intercept; revisions and changing errors are not. DMI is from HadISST, while Nino is from ERSSTv5. We did not check a common-product alternative. Early ocean measurements are sparse. The short test, event dependence and nonstationarity limit precision. No local flood, drought or recovery claim follows from this index test.

## Reproduction and job record

files/REPRODUCE.txt gives commands for a complete offline repeat from the bundled monthly table and a raw-source repeat from the shared data. The package contains 74 annual rows, 175 forecasts across seven variants, code, source hashes, bootstrap draws and a static figure. The independent audit uses a raw, unscaled design and a QR solver. It checks all primary forecasts, season means, score arithmetic and time order. Maximum primary forecast difference is below 1e-14 degrees C. The PNG decodes and meets SCI display limits.

Job: sci-1107-dell-earth-and-ocean-sciences-a34c5f7f58d2. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. One worker did this study. No child agents were launched. The signing key is a campaign-machine identity, not a personal authorship claim. No private key is included. This publication is saved locally; it is not submitted to a remote archive or index.
