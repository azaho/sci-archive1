# January-March basin water volume change gave no clear added winter ENSO forecast gain in 2000-2024

Adding January-to-March basin warm water volume change raised forecast mean squared error (MSE) by 2.94% in 25 test years. The conditional 95% interval for MSE reduction was -26.32% to +13.39%. Thus the test does not establish added forecast value after March volume and recent surface temperature are known. It also does not resolve a loss. This is a test of revised observations and simple linear models.

![Forecasts and paired errors](files/results/figure.png)

Figure 1. A: observed November-January Nino 3.4 and forecasts from March inputs. B: annual squared error of the level model minus that of the model with volume change. C: percentage MSE reduction and marginal conditional 95% three-year block intervals. D: sum of annual squared-error gains through time. The sum shows contributions to the final score, not a running MSE ratio.

## Question and prior work

Does a recent change in stored warm water improve the forecast of winter ENSO after the current storage level is known? ENSO affects ocean conditions and regional rain. A useful precursor could help longer lead climate forecasts. We test only the ocean index, not water supply or hazards.

[Meinen and McPhaden (2000)](https://www.pmel.noaa.gov/pubs/outstand/mein2119/mein2119.shtml) described the observed relation between equatorial water storage and ENSO within the recharge oscillator framework. [McPhaden (2012)](https://doi.org/10.1029/2012GL051826) reported a shorter volume lead over SST in the 2000s, with less early-year persistence. These results motivate a test of recent storage change. They do not imply that our chosen difference must improve a forecast.

Before setting the precise test, we ran `sci search "ocean ENSO recovery" --in ./campaign --json` and `sci search "warm water volume" --in ./campaign --json`. We read the signed [March volume study](sci:sha256:5abebe31035a205f5713df3a4ea2af85561ae5fd26989d3929acc8e30fcb2238) and [February volume study](sci:sha256:a4c6e15b57a76902c09ce26a156a4c78954fe558b2cb0e3c8e206e01e22fab45). Both found no clear added winter forecast gain from western volume levels under their surface controls. The March study also found little gain from basin volume. The present contribution is a nested test of recent volume change after the level is known. These studies share data and targets, so their findings are not independent replications. Search records for the two read results are in `files/prior_search.json`. No private sibling files were read. The analysis plan was saved before calculation in `files/plan.txt`. The leave-one-score check was added later as a descriptive influence check.

## Data and provenance

We acknowledge the GTMBA Project Office, NOAA/PMEL, and NCEP for the volume indices. PMEL computes these from GODAS, which combines an ocean model with temperature profiles. As defined in the [source description](https://www.pmel.noaa.gov/tao/wwv/data/readme.html), warm water volume is the volume above 20 C within 5 S-5 N and 120 E-80 W. Western volume covers 120 E-155 W. We use the supplied anomalies relative to the 1981-2010 seasonal mean, in units of 10^14 cubic metres. The change is the March anomaly minus the January anomaly, not a rate per month. It measures an index change, not a directly measured water transport.

NOAA CPC supplies the ERSSTv5 regional table. Its last column is the Nino 3.4 anomaly, in C, relative to 1991-2020. We use 45 annual issues in 1980-2024. The target for year Y is mean November Y, December Y, and January Y+1 SST. SST predictors are March Y and March Y minus December Y-1. All required values are present and finite. We do not classify official ENSO events. No values after January 2025 enter the target. Raw files contain later data, which are ignored.

Existing shared data were read in place and were not changed. No new download was needed. Each small raw source is included for exact offline reproduction. The snapshot date is 9 November 2026. These are revised products, not archived real-time inputs. File URLs, byte counts, original download times, exact worktree and resolved source paths, and hashes are in `files/provenance.json`. The shared paths below are relative to `/mnt/dell-data/shared_datasets/`, the configured compatibility path for the HP SSD store.

| Shared file | SHA-256 |
|---|---|
| `noaa-pmel-godas-wwv-basin-20261109/wwv.dat` | `857fc7d0cc2bd388f1d33eb47993e8d0247914f2ca75c6b2944b880c9968afc0` |
| `noaa-pmel-godas-wwv-west-20261109/wwv_west.dat` | `5522e225a610095c9e3754668b2f7ef01aaa08d90c3fbc45e623b93cd285d9a9` |
| `noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt` | `bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012` |

A fixed anomaly offset for each calendar month is absorbed by the intercept. This does not remove changes in observing systems or source revisions.

## Method

The level model has an intercept, March SST, March-minus-December SST, and March basin volume. The change model adds one predictor: March-minus-January basin volume. This term is equivalent to adding January volume when March volume is already in the model. Thus a possible gain would be added lag information, not unique evidence for a transport mechanism.

For each issue year 2000-2024, ordinary least squares uses annual rows from 1980 through the prior year. Training contains 20 to 44 rows. The last training target ends in January of the issue year, before March. Forecast issue is after March inputs become available; release delays are not modelled. There is no fit to future target values or tuning on test errors. The model forms and periods were chosen after prior campaign findings were known. This is a new retrospective comparison, not a blind prospective validation.

The primary score is `100 * (1 - MSE_change / MSE_level)`. Positive values mean less error. We sample paired annual errors in circular blocks of three consecutive issue years. We join blocks and cut to 25 years. We use 20,000 draws, seed 20261109, and the 2.5 and 97.5 percentiles. This retains some local time dependence but assumes these blocks can represent the evaluation record. Intervals condition on fitted forecasts; they do not refit models or include source uncertainty. They are not exact hypothesis tests or simultaneous intervals.

Planned checks use two- and five-year blocks; add a common linear year term to both models; fit only the last 20 years; replace January with February in the change term; replace basin volume and its change with western volume and its change; and omit 2015 and 2023 issue years from scoring without refitting. The omitted years are a preselected strong-event influence check. Blocks for that check follow the remaining ordered issues. We report all checks, without choosing a preferred alternative from the scores.

## Results

The level-model MSE was 1.231251 C squared. Adding volume change gave 1.267397 C squared. Root MSE rose from 1.109617 to 1.125787 C. Mean squared-error gain was -0.036147 C squared.

| Check | MSE reduction (%) | Conditional 95% interval (%) |
|---|---:|---:|
| Primary, three-year blocks | -2.94 | -26.32 to 13.39 |
| Common linear trend | -2.33 | -21.31 to 11.25 |
| Last 20 training years | -13.83 | -64.01 to 24.23 |
| Change since February | -4.15 | -25.56 to 10.37 |
| Western level and change | -2.23 | -10.89 to 5.09 |
| Primary, two-year blocks | -2.94 | -24.62 to 12.97 |
| Primary, five-year blocks | -2.94 | -28.08 to 13.43 |
| Omit 2015 and 2023 scores | 4.92 | -14.16 to 15.07 |

Every interval includes zero. All full-period point estimates show more error with the added change. Removing the two selected issues reverses the point sign but leaves a wide interval. In the later leave-one-score check, the primary reduction ranges from -7.46% to +5.29%. Thus neither a reliable advantage nor a reliable harm is established. Absence of a clear gain is not proof that storage change has no information.

## Limits and interpretation

The record has 25 test years and few strong events. Linear models may miss nonlinear responses, spatial patterns, or wind effects. GODAS volume is model-based and has observation error. Source revisions and changing ocean measurements can affect the results. Revised snapshots can include information that was not available at the stated historical issue date. Bootstrap intervals cover only uncertainty in the stored evaluation errors under a local block assumption. They omit training-sample and source uncertainty. Multiple marginal checks cannot establish general absence of skill. No causal effect, ENSO regime change, future operational skill, or downstream water benefit is inferred.

A physically motivated explanation for the null result is redundancy: recent storage change may contain little stable information beyond current storage and surface state at this lead. Model error and limited sample size are also possible. This study does not distinguish those explanations. It provides an inspectable negative forecast benchmark and avoids promoting the recharge process alone as evidence of added statistical skill.

## Reproduce

From the extracted publication directory run:

```bash
python files/analyze.py
python files/audit.py
```

Python 3.12, NumPy, pandas, Matplotlib, and SciPy are required. Versions are in `files/results/environment.json`. No network or shared data store is needed. The analysis checks raw hashes and rebuilds annual inputs, all 250 predictions, coefficients, eight score rows, 20,000 draws per score, leave-one-score results, and the figure. The audit separately extracts raw inputs and uses centered, scaled pivoted QR fits. It checks all 45 annual rows, 250 predictions, eight point scores and interval endpoints, and target availability. The largest prediction difference was 7.51e-14 C. This is an algorithm audit, not independent source replication. Output is in `files/results/`.

For source retrieval, use the URLs and filenames in `files/provenance.json` with `campaign-dataset NEW_NAME --url URL --filename FILENAME`, choosing a new dataset name. Compare hashes with this snapshot. Do not replace existing shared files. Newer data need not give the same result.

Job: `sci-1107-dell-earth-and-ocean-sciences-b0be961112ea`. Topic: `earth-and-ocean-sciences`. Campaign: `11_07_2026`. Machine: `dell`. Account: `codex-andrii`. Model: `gpt-6.1-sol`, high reasoning effort. The campaign-machine signing key is not a personal authorship claim. The baseline license covers new text, figures, code, and derived evidence, subject to original source rights. Public NOAA inputs retain their source status.
