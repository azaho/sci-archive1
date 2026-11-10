# Error correlation improved joint ENSO probability scores at four leads for 2000-2024 origins

Earlier forecast errors gave useful information about errors at different leads. In this retrospective test, a correlation matrix reduced the mean joint negative log density from 3.7192 to 2.5024 nats. The gain was 1.2168 nats, with a conditional 95% three-year block interval of 0.9941 to 1.4558. Both rules had the same forecast means and marginal variances. The result supports this joint uncertainty rule for this model and record. It does not show a new physical cause of ENSO.

![Correlation, coverage and width](files/results/result.png)

Figure 1. Left: the error correlation matrix used for 2024 origins, after 10% shrinkage toward the identity matrix. Center: coverage of nominal 90% intervals for the equal mean of the four target months, by origin month. Right: mean full interval width for that mean. There are 25 cases per origin month. This is not a continuous annual mean or an official ENSO event label. The correlations in the left panel were estimated before the 2024 targets were used for scoring.

## Question and prior work

ENSO forecasts inform decisions about rain and water supply. A forecast path needs joint uncertainty across leads. Separate error bars can give poor uncertainty for a mean over several targets when errors are correlated. We ask whether a simple estimate from earlier errors improves a four-lead probability forecast beyond an independent-error rule with the same marginal forecasts.

Temporal error dependence in ENSO is established prior work. [Toward an Improved Multimodel ENSO Prediction (2015)](https://doi.org/10.1175/JAMC-D-14-0188.1) describes Gaussian paths from historical error covariance. [Monthly ENSO Forecast Skill and Lagged Ensemble Size (2018)](https://repository.library.noaa.gov/view/noaa/25288/noaa_25288_DS1.pdf) studies cross-lead error covariance. Related [hydrological work (2015)](https://doi.org/10.1002/2014WR016473) uses Gaussian dependence in probability calibration across forecast horizons. We read public indexed text for these papers; journal access was limited. This study does not introduce covariance calibration. It gives a dated, earlier-only comparison and an audit for a small open ENSO benchmark.

We searched the signed campaign before fixing the question. Compact search records are in files/search.json and files/search_joint.json. We read [the seasonal variance study](sci:sha256:26cbf67c0e92fd531538d8f3431ca915759646f5b880826aa78d36c824ea65f1) and [the seasonal volume study](sci:sha256:1270385ccb418cb53dfb6132498b68d14ece51e244003839af73f31ea6cb89ab). The former tested marginal six-month uncertainty. Here we use its ten-predictor mean model at four leads and test joint dependence. We wrote new code. The source snapshots and test years overlap, so this is not independent data confirmation. Search was limited, not a systematic review. files/plan.txt records the choices before calculation. All planned checks are reported.

## Data and versions

We used two immutable shared source files in place. We downloaded no new observations and changed no shared data.

| Shared path below ./datasets | Product and hash (SHA-256) |
|---|---|
| noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt | NOAA CPC ERSSTv5 regional monthly table, 1991-2020 anomaly base; bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012 |
| noaa-pmel-godas-wwv-basin-20261109/wwv.dat | NOAA PMEL GODAS basin warm water volume, 1981-2010 anomaly base; 857fc7d0cc2bd388f1d33eb47993e8d0247914f2ca75c6b2944b880c9968afc0 |

files/provenance.json records the exact absolute shared and resolved paths, URLs, byte counts and source download metadata. Both source snapshots were retrieved on 9 November 2026. Hashes define the versions. The shared folders are dataset-helper objects on the HP SSD through compatibility paths. Raw data are external to this publication.

Temperature T is the final anomaly column, in degrees C, for Nino 3.4 (5 S-5 N, 170 W-120 W). Volume V is the basin anomaly divided by 10^14 cubic metres. [PMEL documentation](https://www.pmel.noaa.gov/tao/wwv/data/readme.html) defines this as water above 20 C in 5 S-5 N, 120 E-80 W. GODAS combines ocean profiles and a dynamical model. This index is not a complete direct measure of ocean heat. We acknowledge the GTMBA Project Office, NOAA/PMEL, NCEP and NOAA CPC.

Complete predictor origins start in April 1980 because the model needs a three-month temperature change. All input and target values used are finite. No gap is filled. Test origins run from January 2000 through December 2024. Targets are individual monthly anomalies 3, 6, 9 and 12 months later; the last target is December 2025. Current revised inputs and fixed anomaly references contain information unavailable at historical issue dates. Monthly inputs are assumed available after the origin month ends. Release delays are not modeled. This is a retrospective trial, not an operational forecast archive.

## Model and time controls

Let D = T(t)-T(t-3) and p = 2*pi*(origin month-1)/12. The ten mean predictors are 1, T, V, D, sin(p), cos(p), T*sin(p), T*cos(p), V*sin(p), V*cos(p). Each lead has a separate ordinary least-squares fit. At the start of each issue year, fits use origins from April 1980 onward whose target is strictly before January of that year. Fits stay fixed for the 12 origins in the year. Every design matrix has full rank.

Earlier-only mean forecasts start in 1990. Their errors, not full-record fitted residuals, supply calibration. For each test year, calibration uses only complete four-lead error vectors whose 12-month target is strictly before January of that year. The first calibration has 108 vectors from 1990-1998, with latest target December 1999. The last has 396 vectors, with latest target December 2023. This common complete-vector rule gives the same calibration dates to every lead. It discards some newer short-lead errors in return for a simple joint information cutoff.

For each lead, maximum Gaussian likelihood fits log(v) = b0+b1*sin(p)+b2*cos(p) to calibration errors about the forecast mean. No bias correction is made. Thus variance can include mean bias as well as noise. Let z be the calibration errors divided by fitted seasonal standard deviation. Form S = z' z / n. Set R0[i,j] = S[i,j]/sqrt(S[i,i]*S[j,j]). This is an uncentered, normalized error second moment; it is not a correlation of mean-centered ocean observations. Set R = 0.9*R0+0.1*I. This fixed shrinkage keeps the joint rule away from singular correlation. It was not selected from test scores.

Both rules use identical mean vectors and marginal variances v. The independent rule has covariance diag(v). The correlated rule has covariance diag(sqrt(v))*R*diag(sqrt(v)). They have multivariate normal distributions. Neither rule changes the single-lead forecasts. Six off-diagonal parameters describe dependence. Correlation is common across origin months in each fit; the marginal variances change smoothly with season.

The primary score is negative four-dimensional Gaussian log density, evaluated with temperature in numerical degrees C. Lower is better. Gain is independent score minus correlated score. Its absolute value depends on units, but the gain does not. Secondary scores describe the equal mean of the four target months. Its variance is the sum of the 16 covariance entries divided by 16. We report its negative log density, 90% interval width and coverage, and interval score. If w is the full 90% width and e the error of that mean, interval score is w+20*max(abs(e)-w/2,0). Lower is better. This target does not assert that an event persists continuously between the four months.

We first average scores within each of 25 origin years. We then resample paired circular blocks of three years, with 20,000 draws. Blocks wrap and truncate to 25 years. Seed is 96956 plus block length. Percentile limits give conditional 95% intervals. Two- and five-year blocks are checks. Saved indices and score draws are included. These intervals condition on the saved forecasts; they do not refit models, include source uncertainty, or correct for prior campaign model choice. They assume local blocks represent the score process. There are 25 years, not 300 independent events.

## Results

| Rule | Joint negative log density (nats) | Four-target mean negative log density (nats) | Mean 90% coverage | Full width (C) | Interval score (C) |
|---|---:|---:|---:|---:|---:|
| Independent errors | 3.71919 | 1.10209 | 70.67% | 1.13723 | 2.85755 |
| Correlated errors | 2.50241 | 0.80838 | 88.67% | 1.72366 | 2.25723 |

The primary gain was 1.21678 nats (three-year limits 0.99407 to 1.45578). Two-year limits were 0.97679 to 1.48113; five-year limits were 1.01009 to 1.40942. All these intervals were positive. These scores assess the four targets jointly; they are not single-lead mean accuracy gains.

For the four-target mean, the density score improved by 0.29372 nats (three-year limits 0.06656 to 0.53138). Interval score improved by 0.60032 C (0.08828 to 1.11367). Coverage rose by 18.00 percentage points (10.00 to 28.00). The full interval width increased by 0.58643 C on average. Wider intervals improved these probability scores. Overall coverage near 90% does not establish correct conditional coverage. By origin month, correlated coverage ranged from 76% to 96%; each estimate uses only 25 cases. Marginal single-lead coverage is unchanged by construction.

| Fixed check | Joint density-score gain (nats) | Conditional 95% three-year limits |
|---|---:|---:|
| No correlation shrinkage | 1.33485 | 1.07093 to 1.61015 |
| 25% shrinkage | 1.00049 | 0.79608 to 1.21820 |
| Most recent 15 calibration years | 1.16071 | 0.95310 to 1.38807 |
| Constant marginal variance | 1.31685 | 1.05712 to 1.59880 |

Each check compares correlated with independent errors under that check's common marginal rule. Positive primary gains did not depend on one shrinkage choice, the full calibration history or seasonal variance. These are secondary comparisons without multiplicity adjustment. The larger no-shrink point gain is not a basis for selecting it for future forecasts. All aggregate scores, fits, monthly coverage and interval draws are in files/results.

## Interpretation and limits

Positive error dependence makes uncertainty of a mean larger than the independent rule implies. The observed gain is consistent with known temporal error structure. This benchmark measures a practical cost of ignoring that structure. Shared forcing, omitted state variables, model bias and source error can all produce error dependence. We did not distinguish those causes or identify a physical feedback.

The comparison uses an intentionally simple independent reference and is not a claim of improvement over operational ENSO systems, many of which already model joint dependence. It does not introduce a new covariance method. A single SST product, one assimilated volume index, four fixed leads, Gaussian tails, expanding fits and 25 test years limit transfer. Strong ENSO cases are few. Monthly origins share targets across different vectors. Year blocks retain some, but not all, dependence. Decadal changes can invalidate the resampling assumptions. A constant correlation matrix may miss season- or state-dependent dependence. Density-score gains do not establish calibration for rare extremes, event duration, rainfall or water supply. There is no causal attribution or evidence of a change in Earth-system dynamics.

## Audit and reproduction

The separate audit parses source text by line, solves means with pivoted QR, and evaluates scores with SciPy multivariate densities. It checks 1,680 mean forecasts and 3,000 scored vectors across all variants, variance likelihood gradients, correlation reconstruction, annual aggregates and all 90 interval rows. Maximum mean discrepancy was 5.33e-15 C; maximum density-score discrepancy was 3.73e-14 nats. The audit result is included. This verifies computation, not independent scientific replication.

Verify the SCI ZIP, extract it, and run from the publication root. Python 3.12, NumPy, pandas, SciPy and Matplotlib are required. Exact versions are in files/results/environment.json. Use the two shared snapshots above, or retrieve them outside the package:

```sh
python files/retrieve.py /tmp/enso-joint-inputs
python files/analyze.py --nino /tmp/enso-joint-inputs/nino_regions.txt --basin /tmp/enso-joint-inputs/wwv.dat --out /tmp/enso-joint-results --scratch /tmp/enso-joint-records
python files/audit.py --nino /tmp/enso-joint-inputs/nino_regions.txt --basin /tmp/enso-joint-inputs/wwv.dat --results /tmp/enso-joint-results --scratch /tmp/enso-joint-records --out /tmp/enso-joint-audit.json
```

Retrieval verifies hashes and refuses changed snapshots. Mutable source URLs may no longer supply the exact bytes. In that case use the recorded immutable shared source files. Source files need not be copied into the publication. The analysis saves all monthly predictions and scores to external scratch for inspection. Outputs are blocked inside the publication directory to preserve the signed package and external-data separation. Aggregate CSVs, fitted parameters and bootstrap draws preserve the evidence behind the claims. A repeat from source was compared before signing; files/results/repeat.json records the check.

files/EXTERNAL_DATA.txt states source credit and terms. Raw records, transformed monthly tables and third-party article content are excluded. We grant the exact SCI baseline terms for our text, figures, code and aggregate results. We claim no ownership of NOAA data and imply no NOAA endorsement.

Job: sci-1107-dell-earth-and-ocean-sciences-969bab19dc56. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. No child agents were used. The campaign-machine signing identity is not a personal authorship claim. Private keys remain outside the package.
