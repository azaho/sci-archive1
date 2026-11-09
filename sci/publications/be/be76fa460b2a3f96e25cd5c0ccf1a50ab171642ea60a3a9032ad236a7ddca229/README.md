# Old Faithful intervals alternate in selected 2007-2025 records after source and interval cuts

## Packaging revision — 9 November 2026

This revision supersedes sci:sha256:0660c6bd8579ef0a53f140714dc545f6302d229871f99da6bcd5197b1d40781a for packaging and catalog admission.
The research question, methods, reported estimates and limitations are unchanged.
The event-level datasets are now external references. This bundle contains the
analysis code, aggregate outputs and figures. The external data retain their
original licenses. No source data have been relicensed or deleted.

All mentions below of events.csv.gz, electronic_events.csv.gz, pairs_*.csv,
adjacent_pairs.csv.gz or forecasts.csv.gz refer to external or regenerated
files, not files included in this revision. See files/external-data.json for
the exact excluded-file list and hashes, and files/DATA_NOTICE.md for attribution
and external license terms. The original signed bundle remains available.

We tested short-term memory in Old Faithful eruption intervals from a fixed GeyserTimes archive. In 42,149 adjacent pairs with electronic labels, the correlation after monthly mean removal was -0.332. A strict check used only electronic timestamps. It gave -0.322, with conditional 95% three-month block limits of -0.333 to -0.312. The lag-two correlation was +0.146. The adjacent correlation remained -0.268 when all tested intervals were 80 to 130 minutes. Under an independent event-time error model with zero true adjacent covariance, the strict result would require a timing error standard deviation of 4.91 minutes. Independent one-minute rounding gives only -0.083 square minutes of covariance, against -24.13 observed. This provides a source-filtered benchmark for known serial dependence. It does not identify a physical cause or rule out correlated recording errors. Uneven coverage, event selection, monthly mean removal and unknown sensor errors limit the result. Code, aggregate results, source hashes, a figure, and an audit are included. Event-level data are external, with retrieval and rebuild instructions.

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

Use Python 3.12 with numpy, pandas, scipy, matplotlib and statsmodels. Historical
package versions remain in the original audit or environment JSON. Work from
the extracted revision. Do not run the analysis scripts inside the signed
publication: they generate externally licensed tables. The wrapper copies the
unchanged analysis code to a new scratch directory and runs it there.

To rebuild from the exact raw snapshot:

```sh
python files/reproduce.py --raw /path/to/geysertimes_eruptions_complete.tsv.gz --work-dir /path/to/new-scratch-directory
```

The source URL, snapshot date, size and SHA-256 are in files/external-data.json.
The wrapper refuses a different snapshot. A current download can have changed;
do not treat different bytes as the historical source. The existing campaign
copy is /mnt/dell-data/shared_datasets/geysertimes-eruptions-complete-20261108/geysertimes_eruptions_complete.tsv.gz.

If the exact raw snapshot is unavailable, retrieve the original signed bundle
outside this publication and reproduce from its exact external event tables:

```sh
curl -fL 'https://github.com/azaho/sci-archive1/releases/download/sci-06/0660c6bd8579ef0a53f140714dc545f6302d229871f99da6bcd5197b1d40781a.zip' -o /path/to/original-data.zip
python files/reproduce.py --data-bundle /path/to/original-data.zip --work-dir /path/to/another-new-scratch-directory
```

The wrapper checks the original ZIP hash and every input-table hash before use.
For the raw route it runs all required extraction steps first. Both routes run
the unchanged analysis and audit, then compare the regenerated aggregate outputs
with those included here (relative tolerance 1e-7; absolute tolerance 1e-8).
They write reproduction-check.json in scratch. Event-level outputs remain in
scratch with EXTERNAL_DATA_TERMS.md and must retain the external data terms if
redistributed. The wrapper never writes into the publication or shared source.

This is a reproduction check of the original analysis, not independent scientific
review. The original exploratory scope and uncertainty statements still apply.

## Attribution, license and job

GeyserTimes and GeyserTimes contributors supplied the observations. External
databases retain ODbL 1.0 and their source contents retain DbCL 1.0. The retained
code uses MIT; included text, figures and aggregate results use CC BY 4.0 under
the exact SCI baseline LICENSE. See files/DATA_NOTICE.md and CODE_NOTICE.txt.
The baseline terms do not extend to the linked external databases.

Job: sci-1107-dell-earth-and-ocean-sciences-c6b3eb7f48ee. Topic: earth-and-ocean-sciences. Campaign: 11_07_2026. Machine: dell. Account: codex-andrii. Model: gpt-6.1-sol, high reasoning effort. One finite worker did this investigation; no agents were launched. Analysis dates: 2026-11-08 to 2026-11-09. The signing identity is a campaign-machine key, not a personal authorship claim.

Revision prepared on 2026-11-09 at the campaign owner's request. It preserves
the original job attribution and findings; it does not claim a new experiment.

Both documented reproduction routes were tested on 2026-11-09. Input tables
matched the original hashes, and regenerated aggregate results matched within
the stated tolerances. See files/revision-validation.json. This check does not
establish scientific novelty or independent confirmation.
