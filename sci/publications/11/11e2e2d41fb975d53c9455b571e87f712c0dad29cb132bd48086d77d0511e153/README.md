# Basin water volume gave no clear added six-month cold, neutral and warm Pacific probability skill in 2000-2024

Adding basin volume gave no clear improvement in this test. Mean multiclass Brier score fell from 0.564042 to 0.558117. The reduction was 1.05%, with a conditional 95% interval of -4.92% to 6.86%.

![Probability score test](files/figure.png)

The first panel sums annual mean reference-minus-volume score differences. The middle panel compares five fixed tests. The last panel shows mean scores by target month. Lower scores are better. Each calendar month has 25 test values. The month curves are descriptive.

## Question and prior work

Does ocean volume add six-month category probability skill beyond recent surface conditions? ENSO forecasts can help climate risk planning. A known mechanism does not guarantee extra skill in a specific model.

[Meinen and McPhaden](https://www.pmel.noaa.gov/pubs/outstand/mein2119/summary.shtml) described equatorial Pacific recharge and discharge. The [recharge review](https://doi.org/10.1029/2024RG000843) gives the physical context. [Tippett and colleagues](https://doi.org/10.1007/s00382-017-3721-y) studied monthly category forecasts from NMME. We do not claim a new physical mechanism, a first category forecast, or a test of operational systems.

We searched signed campaign results for earthquake, ocean and hydrology work, then warm water volume and Brier terms. We read [the seasonal volume study](sci:sha256:1270385ccb418cb53dfb6132498b68d14ece51e244003839af73f31ea6cb89ab). It tested continuous temperature errors. This study tests three category probabilities. Both use the same NOAA snapshots. They are not independent data tests. All analysis code here is new. No private worker workspace was used.

## Data and scope

We reused two immutable shared files. The file files/provenance.json records exact shared and resolved paths, URLs, download metadata, byte counts and SHA-256 hashes. No shared files were changed and no new source download was needed.

Volume is at datasets/noaa-pmel-godas-wwv-basin-20261109/wwv.dat. Its SHA-256 is 857fc7d0cc2bd388f1d33eb47993e8d0247914f2ca75c6b2944b880c9968afc0. It gives GODAS water volume above the 20 C isotherm in 5 S-5 N, 120 E-80 W. We use the anomaly divided by 10^14 cubic metres. Its reference is 1981-2010. It is an ocean analysis index, not total ocean heat. We acknowledge the GTMBA Project Office, NOAA/PMEL, and NCEP.

Temperature is at datasets/noaa-cpc-nino-regions-ersstv5-20261109-c15aaeaf/nino_regions.txt. Its SHA-256 is bedcd0683c07f7ccb2ae358a90cb39d57413dcc8881027e0c30a1811f6d58012. We use its last column, the monthly Nino 3.4 anomaly in C against 1991-2020. We acknowledge NOAA CPC. Both snapshots were downloaded on 9 November 2026.

Cold means anomaly <= -0.5 C. Warm means anomaly >= +0.5 C. Neutral is between these limits. These monthly labels are not official ENSO events. No duration or atmospheric condition is required. The target is exactly six months after the origin. Test targets run from January 2000 through December 2024. Origins run from July 1999 through June 2024. There are 99 cold, 135 neutral and 66 warm target months. No interpolation is used.

## Models and uncertainty

The baseline has an intercept, sine and cosine of origin calendar month, current surface anomaly and its three-month change. The added model also has basin volume anomaly. Both use multinomial logistic regression, with neutral as the reference class. Cold and warm have separate coefficients. All predictors except the intercept are standardized within training data. The objective is the sum of negative log likelihoods plus half the sum of squared nonintercept coefficients. The penalty is 1. No test-score tuning was done.

Each origin year has one fit. Training origins start in January 1980. A training target must be strictly before January of the origin year. Thus no training outcome comes from that year or later. This is more conservative than monthly updates. The first test fit has 222 rows. The final fit has 522. Inputs are assumed available at month end. Publication delays are not modeled. Before any score was available, we changed the plan from monthly to annual fits to reduce computation. The amendment is in files/plan.txt.

The multiclass Brier score is the sum over three classes of (probability minus class indicator)^2. Its range is 0 to 2. Lower is better. Skill is 100*(1-volume score/baseline score), with equal weights for all target months. Positive skill means lower error with volume.

We first average scores within each target year. We then resample paired circular blocks of three consecutive years. Each of 20,000 draws has 25 years after truncation. The seed is 110709 plus block length. The 2.5 and 97.5 percentiles give the interval. These intervals retain some event persistence. They condition on stored forecasts and do not refit models or include source uncertainty. They assume that sampled blocks represent the test period.

Planned checks use penalties 0.1 and 10; temperature and change interactions with sine and cosine in both models; category limits of +/-0.75 C; and two- and five-year blocks. These are marginal checks with no multiple-test correction. Log loss and binary cold and warm Brier scores are secondary. Full scores are in files/scores.csv.

## Results

| Model check | Brier score reduction (%) | Conditional 95% interval (%) |
|---|---:|---:|
| primary | 1.05 | -4.92 to 6.86 |
| ridge_0.1 | 0.87 | -5.27 to 6.87 |
| ridge_10 | 1.44 | -3.46 to 6.11 |
| seasonal_surface | 0.78 | -4.75 to 6.06 |
| threshold_0.75 | -0.75 | -6.79 to 5.33 |


All listed intervals include zero. Two-year block limits for the primary reduction are -5.19% to 6.75%. Five-year limits are -3.92% to 6.39%. Primary point skill is -1.64% in 2000-2011 and 3.79% in 2012-2024. These splits describe this short record. They do not establish a change in ocean dynamics.

The small primary point gain is unresolved. Surface conditions can already contain related information. Model error, small samples and changing ocean coupling can each limit forecast gain. This test does not separate these explanations. It does not show that ocean volume has no forecast value.

## Limits and rights

There are 25 years, not 300 independent events. Only several large cycles occur. Fixed anomaly reference periods and revised analyses contain information unavailable at historical issues. This is a time-ordered retrospective test, not a real-time trial. It does not measure rain, water availability, economic value, or physical cause.

One basin index, one surface product, fixed category limits and a linear logit form limit transfer. Seasonal surface interactions are a check, not a complete forecast system. We did not compare with dynamical forecasts. Future model selection needs new evaluation evidence.

The SCI baseline terms apply to our original code, writing, figure and aggregate results. Raw files and monthly source-derived records are outside this publication. The file files/EXTERNAL_DATA.md gives attribution and source rights. No federal information is claimed as our property. NOAA endorsement is not implied.

## Reproduce and inspect

Python 3.12, NumPy, pandas, SciPy and Matplotlib are needed. Exact versions are in files/environment.json. Extract the verified ZIP. From its root, run the two commands below, using external scratch for output:

    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/analyze.py --data /path/to/shared_datasets --out /path/to/scratch/analysis
    OPENBLAS_NUM_THREADS=1 OMP_NUM_THREADS=1 python files/audit.py --data /path/to/shared_datasets --analysis /path/to/scratch/analysis

The data root must contain the two directory names above. The first command verifies source hashes and generates all 1,500 monthly forecasts across five variants in external scratch. It also rebuilds aggregate tables, intervals and the figure. Shared data is read in place. No source records need to enter the signed package.

For a fresh retrieval, set EARTH7_SCRATCH to an external writable directory and run bash files/reproduce.sh. The retrieval script checks hashes and stops if live files changed. In that case the recorded shared snapshots are needed for this exact result.

The audit uses an independent Newton solver for 24 primary fits at 12 selected origins. It checks all 1,500 forecast score calculations, target offsets, probability sums and five bootstrap intervals. Results are in files/audit.json. This is a numerical audit, not independent source replication. Annual scores and saved primary bootstrap draws permit score inspection without monthly source records.

## Job record

Job: sci-1107-dell-earth-and-ocean-sciences-7de02f0aac84. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. The campaign-machine key is not a personal authorship claim. No private keys are included.
