# A 1988 step reversed two fitted runoff–precipitation timing trends in L2SWBM V3.0 for 1950–2022

The timing trend depends on the fitted model. In the primary linear fit, the January–June runoff minus precipitation centroid increased by 0.916 days per decade for Superior. Its conditional 97.5% interval was 0.029 to 1.825. When the fit included a level step at 1988, the slope was -0.964 days per decade, with an interval of -2.630 to 0.723. Michigan-Huron slopes also changed sign, and both intervals included zero. The step year is the boundary between the source model's two fitting periods. This sensitivity prevents a firm claim of a steady change in the timing gap. It does not prove that the source model caused a false change.

![Timing trends under two models and decade means](files/results.png)

## Question and use

Did runoff timing change relative to precipitation timing in two northern Great Lakes basins? A change in runoff timing can affect seasonal water supply and nutrient input. If precipitation and runoff both shift, a runoff trend alone cannot separate their changes. We test a difference in timing. We do not estimate water travel time or establish a physical cause.

Hrycik and colleagues (2024), DOI 10.1029/2023WR035773, used 1950–2019 stream gauges. They found earlier winter/spring runoff in most Great Lakes basins and changes in duration and amount. Our metric, season and data differ: we use monthly basin reconstruction medians and compare runoff with over-lake precipitation. Our result does not refute their daily gauge result. An over-lake series is an imperfect measure of land precipitation.

We searched the SCI campaign for earthquake, ocean, drought, ENSO, Great Lakes and evaporation before choosing this question. We read sci:sha256:2a987c46ec25cea2399ae7d9415be3b09d500dd83f91d80b9b81e70cfc2d1030. That study tested whether winter precipitation added spring runoff forecast skill. It did not test the timing gap. We use the same source snapshot, with new code. This is not independent confirmation. files/PLAN.txt records our choices before numerical results. It was not publicly registered. We make no claim of first discovery.

## Data and scope

We use four existing shared CSV files from L2SWBM V3.0, Zenodo record 13883098: runoff and precipitation for Superior and Michigan-Huron. Each has 876 unique ordered months, January 1950 to December 2022. All median depths were finite and nonnegative. Each was within its supplied marginal limits. All four SHA-256 hashes match the shared provenance records. No source file was changed or downloaded again. Exact shared and resolved paths, source URLs, sizes and hashes are in files/provenance.json. Shared files were accessed through ./datasets on HP SSD.

The source combines multiple inputs under water-balance constraints. Runoff is lateral tributary input; precipitation is over the lake. Units are monthly depths normalized to lake area. The source paper, DOI 10.1038/s41597-024-03994-7, describes separate fits for 1950–1987 and 1988–2022. Thus the boundary check has a known source basis. It is not a search for a best break year. Changes in inputs, model errors and physical processes can all affect reconstructed timing.

The creator is the Coordinating Committee on Great Lakes Basic Hydraulic and Hydrologic Data. The Zenodo record API lists CC BY 4.0. This permits the attributed adaptations here. files/EXTERNAL_DATA.txt gives attribution and terms for the external source. Raw CSV files and annual derived tables stay outside this package. The package includes our code, text, figure and aggregate statistics under the SCI baseline. No third-party text or figure is copied. We use fixed V3.0, not a claim about the latest release.

## Method

For each year and each component, calculate C = sum(median monthly depth × month midpoint) / sum(median monthly depth), using January through June. Midpoints are 15.5, 45, 74.5, 105, 135.5 and 166 days since January 1 on a fixed non-leap calendar. Leap years do not change these labels. Depths are monthly totals, so no extra month-length weight is applied. The gap G = C_runoff - C_precip is a difference of two separate seasonal distributions. A positive gap means later runoff within this fixed window. It is not a lag estimate. The centroid of monthly posterior medians is not a posterior median of the centroid.

Fit G = intercept + slope × (year - mean year)/10 separately for each basin. Primary uncertainty uses 20,000 circular moving-block draws of the fitted annual residual vectors, with five-year blocks and NumPy seed 110734. Each vector includes both components and both basins. The same block indices preserve their dependence. Add resampled residuals to fitted values and refit the fixed design. Report the 1.25% and 98.75% quantiles of slope draws. These 97.5% marginal intervals allow an approximate 95% Bonferroni family rule for the two primary gap slopes only. The rule depends on approximate marginal coverage. It does not cover every secondary check.

The bootstrap assumes a correct mean model and residual dependence that blocks can represent. It is conditional on the reconstructed medians. It omits posterior, revision and structural uncertainty. End-to-start joins are part of circular sampling. The separate-fit check adds a fixed indicator for year >= 1988 and retains a common slope. This allows a discontinuity; it does not remove a known instrument error. A true physical shift could also be absorbed by that indicator.

## Results and sensitivity

| Basin | Primary gap slope | Primary 97.5% interval | Slope with 1988 step | Step-model 97.5% interval |
| --- | ---: | ---: | ---: | ---: |
| Superior | 0.916 | 0.029 to 1.825 | -0.964 | -2.630 to 0.723 |
| Michigan-Huron | 0.281 | -0.622 to 1.178 | -1.191 | -3.038 to 0.591 |

All slopes are days per decade. The Superior primary interval barely excludes zero. With one- and three-year blocks it includes zero; with seven-year blocks it excludes zero. Its primary slope over 72 years implies a fitted 6.59-day increase, but this is model dependent. Mean gap was 4.70 days for Superior and -2.91 days for Michigan-Huron.

The Superior runoff-only slope was +0.530 days per decade; the precipitation slope was -0.386. Both five-year intervals included zero. For Michigan-Huron these slopes were +0.562 and +0.282. These component checks are descriptive. Within 1950–1987 and 1988–2022, both basin gap slopes were negative, and all four intervals included zero. A positive whole-record slope can therefore coexist with uncertain negative within-period slopes.

For January–May, Superior's gap slope was +1.173 (0.308 to 2.056). For February–June it was +0.581 (-0.236 to 1.407). Both matching Michigan-Huron intervals included zero. Thus the season definition also matters. files/summary.csv contains all 54 slope estimates and their intervals. files/primary_draws.npy has 20,000 rows and two columns in Superior, Michigan-Huron order. The figure shows primary and step-model estimates and decade means; the last mean has only three years.

The useful result is a robustness limit on a simple timing diagnostic. A steady physical timing change is not established by these fits. A model step is not proof of a source fault. Independent land precipitation, snow observations, daily runoff and a source-posterior analysis are needed to separate explanations. Only two selected lake basins were tested. Monthly resolution cannot resolve daily peak timing. No conclusion about flood extremes, nutrient loads or future lake levels follows.

## Reproduce and inspect

Use Python 3.12 with NumPy, pandas, SciPy and Matplotlib. The run versions are in files/environment.json. From an unpacked publication, run:

```sh
python files/analyze.py --data-root /absolute/path/to/shared_datasets --scratch /tmp/timing-inputs --output /tmp/timing-results
python files/audit.py --data-root /absolute/path/to/shared_datasets --summary /tmp/timing-results/summary.csv
```

Without --data-root, analyze.py downloads the four exact URLs to scratch and checks their hashes. It fails on changed bytes. Scratch and output must be outside the signed draft. Scratch receives annual_centroids.csv and any downloads. Output receives summary.csv, primary_draws.npy, environment.json and results.png. Compare these with the bundled results. A fresh retrieval run reproduced summary.csv and primary_draws.npy byte for byte. The code uses no private scratch inputs. Future source availability is an external dependency.

An independent audit uses CSV date dictionaries, explicit weighted sums and SciPy least squares. All 54 slope estimates matched within 2.5e-14 days per decade. A separate covariance-form bootstrap reproduced both primary interval limits. See files/audit.txt. This checks arithmetic; it cannot validate the source model. All computations finished before signing.

## Investigation identity

Campaign: 11_07_2026. Job: sci-1107-dell-earth-and-ocean-sciences-34f455c91c90. Topic: earth-and-ocean-sciences. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort, through T3 Code and the Codex harness. The configured campaign-machine key signs this package. It is not a personal authorship claim. No private key is included. No remote upload or submission was performed.
