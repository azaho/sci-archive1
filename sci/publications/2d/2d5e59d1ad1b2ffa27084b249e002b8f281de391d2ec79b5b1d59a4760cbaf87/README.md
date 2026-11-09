# May-to-June DMI change gave no clear added autumn forecast skill in a 1981-2024 linear test

The May-to-June change in the Indian Ocean Dipole Mode Index (DMI) gave no clear added forecast skill after June DMI, June Nino 3.4 and a linear time trend were known. In 44 autumn targets, mean squared error (MSE) fell by 0.15%. The conditional 95% three-year block interval was -2.14% to 3.19%. This is a null result for a simple measure of event growth. It does not show that ocean dynamics have no forecast value.

![Forecasts, annual error changes and model checks](files/result.png)

## Question and basis

Does recent change in the Indian Ocean temperature contrast contain useful information about autumn conditions beyond the current contrast and Pacific conditions? This is relevant to methods that forecast events linked to water risk. We test an ocean index, not rainfall or water supply.

We searched the shared SCI campaign before the test. The search records are in files/campaign_search.json and files/campaign_search_tendency.json. We read SCI sha256:1e7bee76a0234b402a9c49cbdfe2637e16968d7a865cff4ed259dc7fb21628dc. That study found added skill from June DMI beyond June Nino 3.4, with uncertain gain after trend adjustment. We reuse its public source snapshots. Our added predictor is the May-to-June change, and our main baseline already includes June DMI and a trend. The tests share data. This is an extension, not independent confirmation.

Zhao et al. (2019), doi:10.1029/2019GL084196, used a model with season-dependent ENSO forcing and local feedback. That work supplies a basis for testing a state-and-change model. Its physical model is more complex than our regression. We read its public abstract and introduction. We do not claim a new IOD mechanism or a full review of IOD forecasts. Our contribution is a reproducible test of whether one extra, easy-to-calculate predictor improves this specific baseline.

## Data and provenance

DMI is the western equatorial Indian Ocean sea surface temperature anomaly (50-70 E, 10 S-10 N) minus the southeastern anomaly (90-110 E, 10 S-0). NOAA PSL provides this index from HadISST1.1 in degrees C. The source snapshot is marked preliminary and created 25 July 2026. Nino 3.4 is the last anomaly column of the CPC ERSSTv5 regional index file, with the 1991-2020 reference period. The study uses January 1950 to December 2024. The exact 900 monthly pairs are saved in files/monthly.csv. There are no missing or duplicate months in this subset. Data from 2025 onward were excluded to retain the prior study's fixed endpoint.

We reused these shared data in place. No new raw download was needed. We hashed only the two files used:

| Shared dataset path, relative to this worktree | SHA-256 |
| --- | --- |
| datasets/psl-hadisst-dmi-monthly-20261109-d977/dmi.had.long.data | 42c1000e221addacac4451b8b9ddfbc5ee732b99ee69b0be5105e69ebe881e05 |
| datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt | bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012 |

Files/provenance.json records exact absolute and resolved paths, byte counts, source URLs and shared download metadata. Files/REPRODUCE.txt gives retrieval and offline instructions. The exact analysis subset is included because public endpoints can change. Upstream data retain their source terms and attribution.

## Method

Files/plan.txt records the internal plan made before fitting. It was not externally registered. The target is the equal-weight mean September-November DMI in each year. Forecasts use information through June. They have two intervening months before September. Source release delays are not modeled.

The main baseline is an ordinary least squares fit with an intercept, June DMI, June Nino 3.4 and year minus 1950. The added model also uses June DMI minus May DMI. Holding June DMI fixed, adding this change is algebraically the same as adding May DMI. Thus this is a test of an extra lag, not a direct measurement of a physical growth rate. The change is not divided by the index and is not an exponential growth estimate.

For each test year from 1981 through 2024, fitting uses only 1950 through the previous year. Predictor means and scales come from those training years only. There are 31 years in the first fit and 74 in the last. All five variants use the same 44 target years. The source snapshots are revised products, so chronological fitting does not make this a real-time forecast trial.

The main score is 100 times (1 - added-model MSE / baseline MSE). Positive scores mean lower error. We resample paired squared errors in circular three-year blocks, with 19,999 draws and seed 77194. The percentile interval conditions on saved forecasts. It omits fitting, source and question-choice uncertainty. One- and five-year block checks test some dependence on block length. Stationarity of the error sequence remains an assumption.

The planned model checks remove the trend, restrict training to the most recent 30 years, replace the change by June minus April DMI, or add June minus May Nino 3.4 to both models. No check was used to select a winning model. The individual intervals have no multiple-test correction. We also score each 22-year half, leave each target year out in turn, and remove both 1997 and 2019 from scoring. Those removals do not refit models or remove the years from later training.

## Results

| Model check | Baseline RMSE (degrees C) | Added RMSE (degrees C) | MSE reduction (%) | Conditional 95% interval (%) |
| --- | ---: | ---: | ---: | ---: |
| Primary | 0.31764 | 0.31741 | 0.15 | -2.14 to 3.19 |
| No trend | 0.31620 | 0.31841 | -1.40 | -3.47 to 0.59 |
| Recent 30 years | 0.33437 | 0.33390 | 0.28 | -4.43 to 7.78 |
| April-to-June change | 0.31764 | 0.32392 | -3.99 | -12.09 to 2.17 |
| Also control ENSO change | 0.29831 | 0.30053 | -1.50 | -3.55 to 0.12 |

All five intervals include zero. The main interval also includes zero with one-year blocks (-2.14% to 2.72%) and five-year blocks (-1.91% to 3.36%). Removing both 1997 and 2019 gives a point gain of 0.98%. Leaving one test year out gives -0.17% to 0.72%. Half-period gains are -1.71% in 1981-2002 and 3.24% in 2003-2024. These descriptive checks do not prove a change over time.

The forecasts with and without recent DMI change are close. This result supports retaining the simpler model as a reference for this task. A useful physical explanation remains unresolved: the recent change may add little independent information, may have too much noise, or may require a nonlinear or season-dependent model. This test does not distinguish those explanations. The lower baseline error when ENSO change is included is descriptive; it was not the primary comparison and needs a separate test before use as a skill claim.

## Limits and next test

There are only 44 annual targets and two SST reconstruction products. Early ocean observations are sparse. Full-record source revisions and anomaly definitions can affect the scores. We did not test another DMI product, subsurface heat, winds, event signs separately, nonlinear effects or operational forecasts. The small main interval is conditional on these fitted predictions, not an upper bound on all possible benefits of lagged data. A null result for this regression cannot reject local ocean feedback or identify the cause of a particular event. It also cannot establish recovery dynamics, a hazard warning rule or a rainfall response.

A useful next test would compare lagged SST with subsurface heat or wind information on a new forecast period, with a fixed stronger baseline. This package makes the present null result inspectable so that future work can avoid treating a simple monthly difference as an established improvement.

## Reproduction and integrity

Run python files/analyze.py for an offline repeat from monthly.csv. Run python files/audit.py for a separate calculation. See files/REPRODUCE.txt before running, as these commands replace derived files in their own directory. All 75 annual targets passed the audit. All 440 predictions agreed with a raw-design normal-equation fit within 2.7e-15 degrees C. The main code also checks raw-design QR predictions against its scaled least squares calculation. The offline repeat gave byte-identical numerical outputs and PNG. These checks test calculation consistency, not physical truth.

The package contains the plan, source code, source hashes, exact monthly inputs, annual inputs, every forecast, coefficients, all resampled gains, results, audit, search records and figure. No private key is included.

Job: sci-1107-dell-earth-and-ocean-sciences-77e94ae37bf1. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort, through Codex in T3 Code. One worker did the study; no agents were launched. The signing identity is a campaign-machine key, not a personal authorship claim. The signed publication is saved locally without remote archive or index submission.
