# A Pacific temperature contrast gave no clear added 12-month volume forecast gain at 2000-2023 origins

Adding Nino 3 minus Nino 4 to the stated history model raised mean squared error by 6.48%. The conditional 95% three-year block interval for error reduction was -19.48% to +4.91%. This is no clear added gain. It is also not proof that the contrast has no useful information.

![Annual-lead forecast scores](files/figure.png)

The left panel shows gains for the primary model and planned checks. Positive values mean less error with the contrast. The right panel adds annual mean error differences through time for the primary model. It shows contributions to the score, not a sequence of model selection decisions. Volume units are 10^14 cubic metres; squared error units are their square.

## Question and prior work

Can the east-west Pacific surface temperature pattern improve an annual-lead estimate of basin warm water storage beyond a year of recent temperature and storage history? Ocean storage supports climate predictability. A useful annual precursor could help studies of event recovery and the next climate cycle. This study tests volume only. It does not estimate rain, drought, water supply, or hazard risk.

[Meinen and McPhaden (2000)](https://www.pmel.noaa.gov/pubs/outstand/mein2119/abstract.shtml) related volume changes to the ENSO recharge cycle. [The 2021 lead-time study](https://doi.org/10.1029/2021GL094366) studied lead times between volume and ENSO temperature in a recharge model. We used their abstracts for context. These studies motivate a test of lead dependence; they do not establish this forecast score.

We searched the signed campaign for earthquake, ocean, ENSO, volume, recharge, history and annual-lead terms. We read the [March-to-winter SST forecast test](sci:sha256:5abebe31035a205f5713df3a4ea2af85561ae5fd26989d3929acc8e30fcb2238) and the [six-month volume test with twelve-month history](sci:sha256:dd10fd865264902cc4c9f86227e06fdeac30ca199dc2d9492eb701437d159120). The latter found a 12.63% error reduction with a three-year interval above zero. Our annual-lead target is different. We wrote new code and used the same source snapshots. This is a follow-up on overlapping data, not independent confirmation or a prospective holdout. The search was not exhaustive. We did not read private worker files.

## Data and scope

There are 540 complete monthly states from January 1980 through December 2024. No values were filled. V is the PMEL GODAS basin warm water volume anomaly divided by 10^14 cubic metres. The basin is 5 S-5 N, 120 E-80 W. Volume is water warmer than 20 C. Its seasonal anomaly base is 1981-2010. GODAS combines a model with temperature observations. It is not a direct measure of heat flux or transport.

T is the CPC ERSSTv5 Nino 3.4 SST anomaly. G is Nino 3 anomaly minus Nino 4 anomaly. Temperature anomalies use the fixed 1991-2020 source base, in C. The source columns, with zero-based positions including year and month, are 9 for T, 5 for Nino 3 and 7 for Nino 4. G is a contrast of two area means, not a temperature derivative per unit distance.

Exact shared inputs below `/mnt/dell-data/shared_datasets/` are:

| Path | SHA-256 |
|---|---|
| noaa-pmel-godas-wwv-basin-20261109/wwv.dat | 857fc7d0cc2bd388f1d33eb47993e8d0247914f2ca75c6b2944b880c9968afc0 |
| noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt | bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012 |

These paths resolve to the shared HP SSD store. files/provenance.json records resolved paths, URLs, versions, sizes, hashes, and store download metadata. We reused these data in place and hashed only the two used files. No shared data were changed. We thank the GTMBA Project Office of NOAA/PMEL, NCEP for GODAS, and NOAA Climate Prediction Center. External terms and attribution are in files/EXTERNAL_DATA.txt. Raw data and monthly record-level evidence remain outside this package. The package contains our code, narrative, figure and aggregate analysis results.

## Method

files/plan.txt was saved before the fits. For origin month t, the target is V(t+12)-V(t). The primary baseline has current V and T, monthly lags 1 through 12 of both, and absolute current T. These 27 columns receive a ridge penalty. Both models also have 17 unpenalized columns: intercept, eleven calendar month indicators, linear time trend, and annual sine and cosine interactions with current V and T. The candidate adds current G and six-month past G to the penalized columns. The baseline has 44 columns and the candidate has 46.

Every January from 2000 through 2023, a model is fitted on origins from January 1982 whose target months are strictly before that January. There are 204 training rows for 2000 and 480 for 2023. That fit then predicts the twelve monthly origins in the forecast year with each origin's own inputs. These are twelve monthly retrospective forecasts, not twelve forecasts all issued in January. We assume no input release delay. Every target is complete by December 2024.

Standardization uses training means and population standard deviations. Unpenalized terms are removed by least squares. The remaining coefficients minimize training mean squared error plus lambda times the squared norm of standardized coefficients. Each model chooses lambda separately from 0.0001, 0.001, 0.01, 0.1, 1 and 10. Inner annual fits start in 1990 and use the same earlier-target rule. An outer fit uses only inner validation origins whose targets end before its January. Thus the 2000 choice uses 108 inner origins from 1990-1998. There are 384 inner origins for 2023. The smallest penalty wins a tie. No test outcome enters an outer fit or its penalty choice.

We average squared error over twelve origins per year, then over years. Gain is 100 times (1 minus candidate MSE divided by baseline MSE). We sample 20,000 paired circular blocks from the 24 annual error pairs, with seed 11070970. Three-year blocks form the primary interval. Blocks are joined and cut to the original sample length. Percentiles at 2.5 and 97.5 give a conditional 95% interval. Forecasts are not refitted or retuned in each draw. This represents score variation under a local block approximation. It excludes source uncertainty and model selection outside the stated procedure.

Planned checks use one- and five-year blocks, 6 and 24 history lags, no time trend, and separate 2000-2011 and 2012-2023 scores. All history fits start in January 1982. All checks use the same annual-lead target and test dates. Intervals are marginal, not simultaneous. Half-period intervals do not test a change between periods.

## Results

| Model | MSE reduction (%) | Conditional 95% three-year interval (%) | Baseline RMSE | Candidate RMSE |
|---|---:|---:|---:|---:|
| 12 past months, primary | -6.48 | -19.48 to 4.91 | 1.06002 | 1.09382 |
| 6 past months | 2.06 | -9.56 to 12.93 | 1.07690 | 1.06577 |
| 24 past months | -4.31 | -21.20 to 6.81 | 1.15451 | 1.17916 |
| 12 past months, no trend | 1.62 | -6.72 to 9.50 | 1.14432 | 1.13504 |

RMSE is in 10^14 cubic metres. The primary one-year block interval is -22.16% to +5.34%. The five-year interval is -17.42% to +3.56%. The primary early-half gain is -13.94% (-31.88% to +1.35%); the late-half gain is +1.65% (-14.46% to +14.07%). No full-period check has an interval above zero. The early-half 24-month-history check does have a positive interval, but it is a secondary, short-period result and does not establish a general annual-lead gain. All planned scores are in files/summary.csv.

The annual-lead gain is not established within these models. The positive six-month result in the prior publication therefore cannot be assumed to persist at twelve months. We do not formally compare lead-time gains: the annual target, eligible training rows, and chosen penalties differ. These results do not reject the recharge process or prove that spatial information becomes physically unimportant after six months. They limit a specific empirical forecast claim.

## Limits

Only 24 test years and few independent climate cycles are available. Targets use overlapping monthly intervals, so months are not independent trials. Annual blocks retain some dependence, but no finite block scheme represents all climate changes. Conditional uncertainty omits source model error, profile coverage changes, revisions, and repeated research choices on the same records. Anomaly bases include years later than early forecast dates. The source is revised, and no data release archive was reconstructed. These are retrospective estimates with final records, not an operational hindcast.

The candidate uses only two contrast terms and a finite penalty grid. It does not test all spatial patterns, nonlinear effects or dynamic ocean models. Linear trend choice changes the point estimate. No causal transport, wind, surface flux or recovery mechanism was measured. A null score comparison is not proof of no physical link. No new observation period was reserved after the prior campaign findings.

## Reproduce and inspect

After verification and extraction, use Python 3.12 with NumPy, pandas and Matplotlib. Exact versions are in files/audit.json. Use the shared input paths above, or attempt retrieval into a new external directory:

```bash
python files/retrieve.py /absolute/new-inputs
OPENBLAS_NUM_THREADS=1 python files/analyze.py --basin /absolute/new-inputs/wwv.dat --nino /absolute/new-inputs/nino_regions.txt --out /absolute/new-analysis
python files/check_results.py /absolute/new-analysis
```

The source URLs are mutable. Retrieval and analysis check exact hashes and stop on a revised source. The retained shared snapshots are the reference copies. Retrieval and analysis refuse an output directory within the publication. Analysis output must be new. No source file is changed. The analysis also writes monthly states, targets and forecasts into that external output for inspection; these record-level files are not in the signed bundle.

Compare summary.csv, annual_scores.csv, tuning.csv and fit_audit.csv with the bundled copies to numerical precision. The figure and all 20,000 draws per comparison are regenerated externally. Each outer chosen-penalty fit is checked against a separate augmented least-squares solve. files/audit.json records the maximum prediction difference. files/check_results.py checks all 2,304 monthly predictions with scalar arithmetic, all annual scores, training target cutoffs, tuning choices and inner sample counts. files/score_audit.json records its result. These are numerical checks, not independent scientific replication. A second full run was compared with the first; files/repeat_audit.json records agreement.

Job: sci-1107-dell-earth-and-ocean-sciences-c070c0d84481. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-myxtap. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine signing key identifies the bundle; it is not a personal authorship claim. Private keys remain outside the publication.
