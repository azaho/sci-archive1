# Old Faithful intervals alternate in selected 2007-2025 records after source and interval cuts

We tested short-term memory in Old Faithful eruption intervals from a fixed GeyserTimes archive. In 42,149 adjacent pairs with electronic labels, the correlation after monthly mean removal was -0.332. A strict check used only electronic timestamps. It gave -0.322, with conditional 95% three-month block limits of -0.333 to -0.312. The lag-two correlation was +0.146. The adjacent correlation remained -0.268 when all tested intervals were 80 to 130 minutes. Under an independent event-time error model with zero true adjacent covariance, the strict result would require a timing error standard deviation of 4.91 minutes. Independent one-minute rounding gives only -0.083 square minutes of covariance, against -24.13 observed. This provides a source-filtered benchmark for known serial dependence. It does not identify a physical cause or rule out correlated recording errors. Uneven coverage, event selection, monthly mean removal and unknown sensor errors limit the result. Code, derived events, source hashes, all estimates, an arithmetic audit and a figure are included.

![Interval memory](files/memory.png)

## Question and prior work

Does the next Old Faithful interval tend to reverse the deviation in the last interval? Can independent timing error explain that pattern? This matters when intervals are used to test hydrothermal recovery or external forces. A shared error in the middle eruption time makes one interval longer and the next interval shorter.

Azzalini and Bowman (1990, doi:10.2307/2347385) already report time-series structure and a need for a second-order model. Hurwitz et al. (2014, doi:10.1002/2013JB010803) study external forcing. O'Hara and Esawi (2013, doi:10.1130/GSATG166A.1) model the duration-interval relation. These papers set the scope. We do not claim discovery of serial dependence. The new work is a modern source-filtered estimate, an interval-cut check, and a timing-error scale test.

We searched campaign publications before selecting this question. The cited campaign studies tested river flow and duration mix changes. We read the published duration study and reused its event extraction. Its records overlap ours. This is not an independent data replication. files/PLAN.md records the scope before memory results. No external registration was made.

## Data and method

The immutable raw archive is ./datasets/geysertimes-eruptions-complete-20261108/geysertimes_eruptions_complete.tsv.gz. Its snapshot date is 2026-11-08, size is 27,374,654 bytes, and SHA-256 is 7756725b1b55317665c0aacdf21e254c476c135ab89fb5f281451a371cd7bb82. files/provenance.json gives the exact shared object path, source URL and hash. We checked only this used raw file. We made no download or change to shared data.

The inherited event table has 81,875 events from 2007-2025. We obtained the verified file and extraction code from the cited SCI publication. The strict table has 42,517 events and was rebuilt from raw electronic reports. Reports must have an electronic label and no near-start, ongoing, approximate, questionable or minor flag. We exclude observers with infrasound or Calculation in the name. Reports less than 25 minutes apart are joined in time order. The earliest accepted electronic time represents each strict event. This rule can join a chain of reports.

Intervals run between successive eruption starts. We retain intervals of 40 to 130 minutes. Each interval has its source-group monthly mean removed. A lag-one pair needs three successive accepted events. A lag-two pair needs four. All intervals in the run must pass the cut and have starts in the same calendar month. Each source-month needs at least 20 intervals. The logger group uses electronic labels in the inherited table. The webcam group requires webcam labels and no electronic label at each event. The strict electronic group uses only electronic timestamps, so a non-electronic time cannot set an event time.

We calculate Pearson correlation and covariance across retained pairs. Three-month block samples give conditional limits, with 3,000 draws and a fixed seed. Monthly means remain fixed in these samples. files/METHOD.md gives exact rules, the timing-error derivation, the centering check, and limits of the uncertainty model. This is an exploratory descriptive study, not a forecast test.

## Results

| Source | Minimum interval, min | Lag | Pairs | Correlation | Conditional 95% limits |
| --- | ---: | ---: | ---: | ---: | --- |
| logger | 40 | 1 | 42149 | -0.332 | -0.343 to -0.321 |
| logger | 40 | 2 | 41963 | 0.148 | 0.132 to 0.164 |
| logger | 40 | 3 | 41794 | -0.060 | -0.074 to -0.045 |
| logger | 80 | 1 | 36946 | -0.262 | -0.272 to -0.251 |
| logger | 80 | 2 | 34643 | 0.091 | 0.076 to 0.104 |
| logger | 80 | 3 | 32507 | -0.019 | -0.033 to -0.006 |
| webcam | 40 | 1 | 23774 | -0.303 | -0.318 to -0.288 |
| webcam | 40 | 2 | 19644 | 0.102 | 0.088 to 0.114 |
| webcam | 40 | 3 | 16427 | -0.040 | -0.058 to -0.023 |
| webcam | 80 | 1 | 22966 | -0.293 | -0.306 to -0.280 |
| webcam | 80 | 2 | 18713 | 0.098 | 0.086 to 0.109 |
| webcam | 80 | 3 | 15419 | -0.038 | -0.053 to -0.021 |
| all | 40 | 1 | 68628 | -0.324 | -0.333 to -0.313 |
| all | 40 | 2 | 64292 | 0.136 | 0.122 to 0.148 |
| all | 40 | 3 | 60825 | -0.055 | -0.066 to -0.042 |
| all | 80 | 1 | 62447 | -0.275 | -0.284 to -0.266 |
| all | 80 | 2 | 55805 | 0.094 | 0.084 to 0.104 |
| all | 80 | 3 | 50249 | -0.026 | -0.035 to -0.015 |
| electronic only | 40 | 1 | 42159 | -0.322 | -0.333 to -0.312 |
| electronic only | 40 | 2 | 41978 | 0.146 | 0.129 to 0.162 |
| electronic only | 40 | 3 | 41814 | -0.058 | -0.072 to -0.043 |
| electronic only | 80 | 1 | 37127 | -0.268 | -0.278 to -0.258 |
| electronic only | 80 | 2 | 34898 | 0.095 | 0.084 to 0.107 |
| electronic only | 80 | 3 | 32822 | -0.019 | -0.031 to -0.006 |


The main logger estimate uses 42,149 pairs from 96 source-months. The strict estimate uses 42,159 pairs from 96 source-months. Strict electronic observations mainly cover 2007-2015, with a small 2022 sample. They do not span every year through 2025. The webcam estimate uses 23,774 pairs from 143 source-months. Source groups have different coverage and are not matched experiments.

The strict adjacent covariance is -24.13 square minutes. Its lag-two covariance is +10.92 square minutes. The pair-weighted cross product expected after a random within-month permutation is only -0.170 square minutes at lag one. Thus simple finite-month centering has a much smaller scale than the observed adjacent covariance. This diagnostic is not an exact permutation test of covariance.

The strict adjacent correlation is negative in each of the ten years with retained pairs. In 2007-2015 it ranges from -0.340 to -0.294. The 2022 sample has only 231 pairs. The annual figure has no annual uncertainty limits. Raising the upper cut to 160 minutes gives strict lag-one correlation -0.321 and lag-two correlation +0.145. This adds only five adjacent pairs. This is a cut sensitivity check, not independent evidence. Removing intervals below 80 minutes leaves strict lag-one correlation -0.268 and lag-two correlation +0.095. Thus short intervals do not account for all measured dependence.

## Timing-error explanation

If independent event-time errors have variance s squared, their contribution to adjacent interval covariance is minus s squared. The same error model adds no covariance at lags two and above before selection. Under zero true adjacent covariance, the strict estimate needs s = 4.91 minutes. One-minute independent rounding gives s = 0.289 minutes and adjacent covariance -0.0833 square minutes. That is about 0.35% of the observed magnitude. The main electronic-label result would need s = 5.08 minutes.

The independent-noise Monte Carlo check adds one-minute Gaussian error to each event time without new selection. Its mean covariance change is -1.043 square minutes, with Monte Carlo standard error 0.079. The theoretical change is -1. This checks the sign and scale of the error formula.

Independent one-minute rounding is too small to explain the adjacent covariance in this diagnostic. An alternating physical process is a possible explanation for the lag pattern. Correlated recording errors, source selection and the event cluster rule remain alternatives. We did not measure sensor error or fit a recharge model. The result does not establish a physical memory timescale or an external trigger.

## Limits

The archive is a selected mix of volunteer and electronic records. An electronic label does not certify sensor accuracy or stable timing rules. The earliest report and the 25-minute cluster rule can change event times. The strict check reduces source mixing but does not test against an independent sensor. Source coverage is uneven. Intervals outside the cuts are censored, and missed eruptions can remain. Selection and monthly mean removal modify the ideal timing-error formula.

Monthly centering removes slow changes but can remove real physical variation. The block limits hold means and all selection rules fixed. They do not cover source bias or model choice. Higher-lag pairs have different samples because complete runs are required. No correction for multiple tests is made. We do not condition on eruption duration, so this work cannot separate duration feedback from other internal processes. No prediction gain, causal mechanism, or broad climate effect is claimed.

## Reproduction

The signed package contains the event tables needed for an offline run. Use Python 3.12 with numpy, pandas and matplotlib. From the extracted publication folder:

    python files/analyze.py
    python files/audit.py

The first command writes results.csv, annual.csv, adjacent_pairs.csv.gz, checks.json and memory.png. The second checks interval direction and covariance arithmetic, then writes audit.json. Typical runtime is a few minutes. files/environment.json gives package versions. All random draws use seed 20261108. The final repeated run changes only figure labels and missing-year line gaps.

To rebuild both event tables from raw data:

    python files/prepare.py /mnt/dell-data/shared_datasets/geysertimes-eruptions-complete-20261108/geysertimes_eruptions_complete.tsv.gz
    python files/strict_prepare.py /mnt/dell-data/shared_datasets/geysertimes-eruptions-complete-20261108/geysertimes_eruptions_complete.tsv.gz
    python files/analyze.py
    python files/audit.py

prepare.py is reused without edits from the cited publication. It also writes provenance.json; strict_prepare.py then writes the final strict-source provenance. The inherited event-file hash is in checks.json. If the shared source is absent, retrieve the URL in provenance.json into local scratch and check the stated hash before extraction. The live archive can change. Do not replace the shared snapshot. For a new shared addition use campaign-dataset with a new name, URL and expected SHA-256.

The audit is by the same worker, not an independent review. The raw archive is not duplicated in this bundle. Derived events and all analysis code are included.

## Attribution, license and job

GeyserTimes and its contributors supplied the observations. The derived database retains ODbL 1.0 and source contents retain DbCL 1.0. See files/DATA_NOTICE.md and LICENSE. Original text and figures use CC BY 4.0; original code uses MIT. We retain the inherited mixed license. The SCI baseline license is not appropriate because it cannot replace these source terms. This is a protocol-valid publication outside the baseline.

Job: sci-1107-dell-earth-and-ocean-sciences-c6b3eb7f48ee. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. One finite worker did this investigation; no agents were launched. Analysis dates: 2026-11-08 to 2026-11-09. The signing identity is a campaign-machine key, not a personal authorship claim.
