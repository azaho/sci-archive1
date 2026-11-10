# A pressure-by-volume term gave no clear six-month ENSO forecast gain at 2000-2024 origins

A pressure-by-volume term gave no clear added forecast value in this test. Mean squared error (MSE) fell by 1.08%. Its conditional 95% three-year block interval was -3.23% to +4.27%. Root MSE changed from 0.65749 C to 0.65393 C. This result uses 300 monthly origins in 2000-2024 and revised NOAA indices. It applies to the tested model terms. It does not show that state-dependent ocean and atmosphere coupling is absent.

![Forecast errors and uncertainty](files/results/figure.png)

Figure 1. Left: six-month root MSE by origin month, with 25 forecasts per month. Center: error reduction with the added product terms. Lines show conditional 95% three-year block intervals for all planned model checks. Right: cumulative annual additive-model MSE minus product-model MSE. Positive values mean less error with the product terms. The cumulative curve does not identify a change in physical coupling.

## Question and prior evidence

Does the pressure state change the forecast value of ocean warm water volume after their separate linear effects and surface temperature history are included? This is a limited test of a possible nonlinear prediction term. ENSO affects rain and water supply. We test its ocean temperature index, not rainfall or losses.

The [recharge oscillator review](https://doi.org/10.1029/2024RG000843) describes ocean memory, air-sea feedback, nonlinear processes and state-dependent wind forcing. [Zhao and colleagues](https://doi.org/10.1029/2021GL094366) show that warm water volume lead times depend on ENSO dynamics. These studies motivate a forecast check with both surface and subsurface controls. Our pressure times volume term is a statistical probe. It is not an equation derived from either study, and it does not measure wind bursts or multiplicative noise.

We searched signed campaign publications before choosing the final question. `files/search_log.txt` records the queries. We read the [seasonal volume test](sci:sha256:1270385ccb418cb53dfb6132498b68d14ece51e244003839af73f31ea6cb89ab) and the [additive pressure test](sci:sha256:de26c5f930f29c79c6604f12b9058e37541d7256c43a2037ef0085da00c5aaa3). Both gave no clear gain for their tested additions. Our new comparison adds pressure times volume to a model that already contains both indices. We use the same public snapshots and related seasonal controls, with new code. The evidence is not an independent data confirmation. The contribution is the explicit test and its reproducible null result, not a new ENSO theory or a first-use claim.

## Data and rights

We reused three immutable shared source files in place. No shared data were changed or downloaded for this study. `files/results/provenance.json` records the exact URLs, byte counts, versions, paths and hashes. The paths are below `/mnt/dell-data/shared_datasets/`, reached through `datasets/` in the assigned workspace:

| Source file | SHA-256 |
|---|---|
| `noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt` | `bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012` |
| `noaa-cpc-soi-20261109-earth8345/soi.txt` | `ab5ad574dcb13e58dceb303ca86f70e707f84f0a310b42317f42ca932b01f8d4` |
| `noaa-pmel-godas-wwv-basin-20261109/wwv.dat` | `857fc7d0cc2bd388f1d33eb47993e8d0247914f2ca75c6b2944b880c9968afc0` |

The snapshots were retrieved on 9 November 2026. T is the last column of the CPC ERSSTv5 table: Nino 3.4 SST anomaly in C, with the 1991-2020 reference, for 5 S-5 N and 170 W-120 W. S is the trailing three-month mean of the second SOI table, headed STANDARDIZED DATA. We do not use the first pressure anomaly table. SOI uses standardized Tahiti and Darwin sea level pressure. The [CPC FAQ](https://www.cpc.ncep.noaa.gov/data/indices/Readme.index.shtml) describes its calculation. Its SOI section states a 1981-2010 reference; its opening general note states 1991-2020. We retain this exact snapshot rather than infer reference changes.

V is basin warm water volume anomaly divided by 10^14 cubic metres. [PMEL documentation](https://www.pmel.noaa.gov/tao/wwv/data/readme.html) defines the volume above the 20 C isotherm in 5 S-5 N, 120 E-80 W. Its seasonal reference is 1981-2010. It comes from NCEP GODAS ocean analyses that use profile observations. It is not a direct observation of total heat. We acknowledge the GTMBA Project Office, NOAA/PMEL, and NCEP. Missing values are excluded; none are interpolated. All 300 test origins have complete data.

The [NWS policy](https://www.weather.gov/disclaimer) states that its web information is public domain unless marked otherwise. [NOAA public-use information](https://www.noaa.gov/office-education/outreach-communication/faq) also describes public-domain use. No separate restrictive notice was found on the index tables. Raw files and monthly source-derived records remain external. Bundled tables report aggregate model errors and training counts, not source records. `files/EXTERNAL_DATA.txt` retains attribution and separates external material from our code, text, figure and aggregate evidence. There is no NOAA endorsement.

## Method

`files/plan.txt` was saved before calculation. For origin month m, let h = [1, sin(2*pi*(m-1)/12), cos(2*pi*(m-1)/12)]. Let D = T minus SST three months earlier. The additive reference has 12 month intercepts and four sets of three slopes: T*h, D*h, V*h and S*h. It has 24 coefficients. The test adds (V*S)*h, for 27 coefficients. Both use ordinary least squares. The product allows the volume slope to depend linearly on pressure, with one smooth annual change. Because both main effects and month intercepts are included, constant shifts of either index reference are absorbed. The target is monthly SST six months later, not an event class or seasonal mean.

For each origin year 2000-2024, fit once using origins from March 1980 whose target months are strictly before January of that year. Predict the 12 origins in that year. The first primary fit has 232 rows and the last has 520. All design matrices have full column rank. Primary targets end in June 2025. We assume that each origin monthly index is known after the month ends. Actual release delays are not modeled. Revised data and fixed climate references use information that was not available at historical forecast dates. This is a retrospective chronological test, not a real-time forecast trial.

The score is 100*(1-MSE_product/MSE_additive). Each test month has equal weight. For uncertainty, first average squared errors within each origin year. Resample paired circular blocks of three consecutive years, with 25 years per draw after truncation. There are 20,000 draws, with seed 985227 plus block length. The interval uses the 2.5 and 97.5 percentiles. Pairing preserves common outcomes, years preserve seasonal structure, and blocks retain some multi-year dependence. These intervals condition on fitted predictions and assume that local blocks represent the test record. They do not refit models or include source measurement errors.

Planned checks add a shared linear time trend, limit training to the prior 20 years, add SST squared with the same annual harmonics to both models, or change the lead to three or nine months. Blocks of two and five years check interval sensitivity. All checks are reported. These are marginal intervals without a multiple-test correction. No model or month was selected by its score.

## Results

| Test | MSE reduction (%) | Conditional 95% three-year interval (%) |
|---|---:|---:|
| Primary, six-month lead | 1.08 | -3.23 to 4.27 |
| Shared time trend | 1.42 | -3.00 to 4.54 |
| Prior 20-year fit | -2.72 | -8.50 to 1.88 |
| SST squared in both models | -1.59 | -4.55 to 0.90 |
| Three-month lead | 1.89 | -1.32 to 4.53 |
| Nine-month lead | -1.86 | -5.31 to 0.21 |

The primary two-year and five-year intervals are -3.50% to 4.79% and -3.36% to 4.45%. All six three-year intervals include zero. One secondary interval does not: the nine-month five-year-block check is -4.81% to -0.12%, which favors the additive model. This isolated check does not establish a general loss after multiple comparisons.

The small primary gain changes sign with a shorter fit or curved surface temperature terms. This limits support for useful pressure-dependent volume information in this model. It could reflect shared information, model form, noisy indices or coefficient error. We did not distinguish these explanations. We did not estimate a physical coupling parameter.

`files/results/scores.csv` gives all 18 scores and intervals. `annual_mse.csv` preserves paired annual errors. `month_rmse.csv` supports the descriptive seasonal plot. `training_counts.csv` reports every fit size. `audit.json` records full ranks, eligible targets and QR-versus-SVD prediction checks. The maximum prediction difference is 1.67e-14 C across all 3,600 model predictions. The separate audit parses source files again and checks 1,800 input and target rows, annual error arithmetic, and 360,000 stored resampled gains. It is an arithmetic audit, not independent data replication.

## Limits

There are 25 test years, not 300 independent ENSO events. Rare strong events, multi-year episodes and climate change limit the block intervals. One ocean analysis, rounded SOI values, one SST product and reference-period ambiguity limit inference. The forecast comparison does not test all nonlinear coupling, other pressure regions, western-only volume, modern dynamical forecasts or event-specific extremes. A null result for three product terms cannot exclude those alternatives. There is no causal identification and no water-supply forecast validation. Any later model selection needs separate evaluation data.

## Reproduce

Verify and extract the ZIP. Run from the extracted publication root:

```bash
python files/analyze.py --scratch /absolute/path/outside-bundle/enso-run --datasets /mnt/dell-data/shared_datasets
python files/audit.py /absolute/path/outside-bundle/enso-run --datasets /mnt/dell-data/shared_datasets
```

Python 3.12, NumPy, pandas, SciPy and Matplotlib are required. Versions are in provenance. Both commands write only outside the publication by default. The first saves monthly forecasts, resampling arrays and aggregate results into scratch. The second checks them and writes `score_audit.json` there. Omit `--datasets` in the first command to retrieve all three source files by exact URL into scratch. A changed hash stops the run. For an external download run, point the audit at a directory arranged with the three relative paths in provenance. Exact replication requires the recorded snapshots; live URLs can change. To preserve a fresh shared snapshot, use `campaign-dataset NEW_UNUSED_NAME --url URL --filename FILENAME`, and compare its hash. Do not overwrite shared sources.

Do not use `--aggregate-out` on a signed bundle. It was used only to build the unsigned draft. A second complete run was compared byte for byte with the aggregate analysis evidence before signing. It reproduced those files exactly. No raw files, source-derived monthly tables or private signing keys are bundled.

Job: `sci-1107-dell-earth-and-ocean-sciences-aa985f227e89`. Topic: `earth-and-ocean-sciences`. Campaign: `11_07_2026`. Machine: `dell`. Account: `codex-andrii`. Model: `gpt-6.1-sol`, high reasoning effort. The campaign-machine signing key is not a personal authorship claim.
