# Past SST predictions add a cloud-linked radiation signal under cubic time controls in five CMIP6 families

Job: sci-1107-dell-earth-and-ocean-sciences-2816f42ca39e. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-olen. Model: gpt-6.1-sol, high reasoning effort. The signing key identifies a campaign machine. It does not claim personal authorship.

## Question and scope

Can the excess radiation response in the published AMIP-minus-HighResMIP comparison be described as an immediate scalar gain? We test whether past and future SST-based predictions add information after the current prediction, sea ice and time controls are fitted. We use the existing 1980-2014 monthly table from seven model pairs. We average related resolutions into five model families. No new model run or observation is used.

The original comparison, SCI 96a66d04, found radiation gains above the mean of five Green's functions. SCI fc80ab91 found that the signal is shared across families. SCI 6ec7809f and 27de4f26 showed that transfer to unused time periods is uncertain. Here, we test timing rather than repeat those gain tests. The GFMIP protocol describes limits of linear spatial response maps, including nonlinear response (doi:10.1029/2023MS003700). Our timing test cannot identify the cause of a map error.

## Results

The present-month gain is **1.063**, with a conditional 95% interval of **0.681-1.448**, when the preceding and following three-month mean predictions are also fitted. The past coefficient is **0.650 (0.164-1.112)**. The future coefficient is **0.246 (-0.227 to 0.717)**. Thus, the data resolve an added past signal in this model, but do not resolve an added future signal. An instantaneous prediction with unit gain is not excluded for the present term alone.

![Timing coefficients in monthly and annual fits](files/timing.png)

| Fit or component | Past coefficient | Present coefficient | Future coefficient |
|---|---:|---:|---:|
| Monthly total radiation | 0.650 [0.164, 1.112] | 1.063 [0.681, 1.448] | 0.246 [-0.227, 0.717] |
| Monthly clear-sky radiation | 0.170 [-0.108, 0.464] | 0.837 [0.618, 1.055] | 0.081 [-0.210, 0.368] |
| Monthly all-sky minus clear-sky | 0.480 [0.121, 0.829] | 0.226 [-0.062, 0.513] | 0.165 [-0.185, 0.537] |
| Annual total radiation | 0.875 [0.253, 1.506] | 2.179 [1.597, 2.776] | -0.337 [-0.999, 0.392] |

All coefficients are dimensionless: both radiation and its prediction use W m-2. Monthly neighbors are three-month means. Annual neighbors are single adjacent years. The two fits have different time resolution and cannot be interpreted as the same transfer kernel.

The all-sky-minus-clear-sky term supplies **74% of the point past coefficient**. Its past coefficient excludes zero in the stated resampling scheme. This term is a cloud radiative effect difference. It includes cloud masking of other effects and is not a pure cloud feedback. The source table has no separate clear-sky Green's-function prediction, so we cannot assign the Green's-function *error* to clouds. Component coefficients add to the total to numerical precision.

The annual same-year gain remains above one when both adjacent-year predictions are fitted. The annual estimate uses 33 target years, 1981-2013, and predictors from 1980-2014. Starting the input record in 1985 gives a same-year gain of 1.724 [1.014, 2.439]. The excess annual response therefore does not vanish when neighboring years are controlled. This supports the prior in-record gain result within the tested regression model.

## Sensitivity and a prediction check

With cubic controls, past-window lengths of 1, 3, 6 and 12 months give positive mean past coefficients. Their conditional intervals all exclude zero. Present coefficients range from 1.035 to 1.199 and their intervals include one. None of these future coefficients has an interval that excludes zero. Changing residual block length from 24 months to 12 or 36 months has little effect on the main three-month intervals. Starts in 1985 and 1994 retain positive past coefficients with intervals above zero.

Time controls matter. With an intercept and no time polynomial, the three-month future coefficient is 0.507 [0.002, 0.996], with a marginal two-sided null probability of 0.049. A linear or cubic time control removes this weak result. It is one of several exploratory tests and does not establish anticipation. The cubic-control future null probability is 0.296. A failure to reject zero does not show that all confounding is absent.

We also compare two retrospective prediction models: present prediction alone versus present plus the past three-month mean. Both fit the same sea-ice and time controls on the training rows only. We leave out six-year blocks, with a one-year gap on each side. The final block is five years. All fits use both earlier and later training years when available. These are tests of an atmosphere-model response given SST predictors, not operational SST or weather forecasts.

With cubic time controls, the past term reduces pooled held-out mean squared error by **4.66%**. A three-year block interval on the saved annual loss pairs is **1.32-7.66%**. All five family point gains are positive. Omitting the endpoint folds reduces the gain to **1.81% [0.31, 3.35%]**. With linear time controls, the pooled gain is **-0.82% [-2.65, 0.79%]**; the interior-only gain is **0.74% [-0.79, 2.22%]**. Thus, prediction evidence depends on the time control. These loss intervals condition on fitted predictions and do not include calibration uncertainty. They do not establish a robust predictive improvement. This extends, rather than removes, the limits found in the prior transfer studies.

## Method

For each family, fit

    y(t) = time polynomial + b_ice I(t)
           + b_past mean[g(t-1), ..., g(t-h)]
           + b_present g(t)
           + b_future mean[g(t+1), ..., g(t+h)] + error(t).

Here y is net downward AMIP-minus-HighResMIP radiation, g is the published five-function SST prediction, and I is the published sea-ice term. The primary display uses cubic time and h=3 months. The annual check uses h=1 year. The four time columns are 1, t, t squared and t cubed; t spans -1 to 1 over each input period. All coefficients, including the ice coefficient, are fitted separately in each family. We then take an equal-family mean of the fitted coefficients. This is not the cross-family covariance-ratio estimator in SCI fc80ab91.

CNRM averages the CNRM-CM6-1 and CNRM-CM6-1-HR pairs. HadGEM averages its LL/LM and MM pairs. GFDL, IPSL and MPI each supply one family. All retained family months are present. We use 1980-2014 to obtain a common record. The primary monthly targets are April 1980 to September 2014 (414 months). Annual means weight the twelve months equally. Source anomalies and predictor definitions are retained. The source Green's functions cover ice-free SST at 60 S to 60 N.

We make 4,000 circular moving-block residual draws, seed 281642, with the same time indices for all five families. Each draw retains the fitted time, ice and predictor signal, adds resampled residuals, and refits all coefficients. This preserves shared residual changes across families. The design and predictors are fixed. Monthly primary blocks have 24 rows; annual blocks have three rows. The future-term null test uses residuals from a restricted fit with that term omitted. Its probability compares the absolute mean future coefficient with the corresponding restricted bootstrap estimates. Intervals are marginal percentiles, not simultaneous intervals. They assume residual blocks can be moved in time. They are descriptive conditional intervals, not full climate uncertainty.

The holdout check uses seed 281643 and 4,000 three-year circular block draws of annual mean loss pairs. Loss resampling does not refit calibration. The saved code regenerates the monthly loss file into separate scratch; it is not bundled. Interior folds cover 1986-2009. Both tests use exploratory choices made after initial timing fits. No test was registered in advance.

Independent numerical checks use the Frisch-Waugh-Lovell residual formula for every future coefficient and the exact additive component-slope identity. Both pass. `timing.csv` gives all family estimates, case choices, conditional intervals, condition numbers, null probabilities and the in-sample future-term error change. `bootstrap.npz` preserves coefficient draws. `holdout_summary.csv` gives the separate prediction check.

## Interpretation and limits

A signal from past SST predictions can arise from atmospheric adjustment, from SST patterns not represented by the scalar predictor, or from changes in model forcing and setup that correlate with the predictor. The results do not distinguish these explanations. They do not measure an atmospheric response time. The 12-month window result is a window sensitivity test, not evidence for year-long cloud memory. Future-prediction coefficients are diagnostic associations, not causal effects.

The source model pairs differ in more than SST: daily versus monthly forcing, start dates, and some atmospheric forcing or configuration details. The GFDL pair differs in atmospheric resolution. Clear-sky differences also flag possible forcing differences. Models and resolutions are related. Single HighResMIP members carry internal noise. Cubic controls can remove real slow SST response, while weaker controls can leave forcing differences. None of these data identifies the correct SST product.

This work gives a reproducible timing audit and evidence for an added past, cloud-linked radiation signal under stated controls. It retains the annual excess-response finding but does not support use of its ratio as an immediate, general multiplier for an SST artifact correction. It does not estimate climate sensitivity or validate a new SST correction.

## Data, rights and reproduction

The only numerical input is `files/data/pair_series_monthly.csv.gz` in source SCI publication `sha256:96a66d04c75df7c97e71eb3d97a5d79e109a0c0d3eed2d9aa855cd062c8ca119`. The exact archive path is `/mnt/dell-data/campaigns/11_07_2026/96a66d04c75df7c97e71eb3d97a5d79e109a0c0d3eed2d9aa855cd062c8ca119.zip`, reached through `./campaign`. The entry SHA-256 is `94ba20761c0ff3ea514a739063984188233401bb496a2630e26b2a78f8d90e6e` (165,721 bytes). The archive was verified before use. `files/source_verify.json` records that check. The source archive preserves original CMIP6 store versions, reduction code, notices, and predictor provenance. No raw file under `./datasets` was used or downloaded. The analysis does not depend on private scratch after publication.

Use Python 3.12 with NumPy, pandas and Matplotlib. Tested versions are recorded in `files/provenance.json` (NumPy 2.5.4, pandas 3.1.1). Obtain and verify the cited source archive with SCI. Extract this package's own code to a location of your choice. In a separate scratch directory, set CODE to the absolute path of its `files` directory and CAMPAIGN to the archive directory. Run `sh "$CODE/reproduce.sh"`. It verifies the input and writes all outputs to `./regenerated`. The main script also checks the input entry hash. Run with one numerical library thread; no more than two CPUs are needed. The full repeat took a few minutes on the assigned host.

Only new code, text, figures, fit summaries and resampling draws are included. External time series and record-level derivatives remain outside this package. See `files/NOTICE.md` for source credit and external data terms. The exact SCI baseline license is unchanged.
