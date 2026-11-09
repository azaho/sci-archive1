# Zero bleaching accounted for 996 of 1,052 exact depth matches in Reef Check surveys from 1998 to 2019

## Question and prior work

How much numerical separation do archived bleaching values retain between depths at the same site and date? This matters when these records are used to test whether deeper reefs provide a refuge from marine heat stress.

Field studies found depth-related differences in the Maldives (doi:10.1098/rspb.2017.1551) and limited thermal refuge on the Great Barrier Reef (doi:10.1038/s41467-018-05741-0). Their reef communities and depth ranges differ from ours. Our audit does not retest those field results.

We began SCI campaign searches before the precise question. The SCI bleaching search completed successfully; its full record is in files/campaign_search.json. A metadata scan of published ZIPs found prior depth and missing-value reports. We read both with sci read. SCI 4a789955ad022aafa7fda357e761144e3c74ab8788fe72415b219ba6fe1192b4 found small mean depth contrasts. SCI 9b3ffec519c0e56efbde48e2ac9391ffae1858ba280459177d75d2b6bd9e575c bounded missing outcomes. We therefore changed from another mean-depth analysis to this numerical agreement audit. Observations overlap. This is not independent data replication or a new general method. It adds a reproducible archive diagnostic.

## Data and comparison

We used BCO-DMO 773466 version 2, dated 2022-10-14, in the shared Global Coral-Bleaching Database CSV. The source methods are in doi:10.1038/s41597-022-01121-y. There are 41,361 raw rows. We held the broad survey source fixed at Reef Check.

Repeated Reef Check sample identifiers must agree in depth, bleaching, date, site and heat. The code checks this, then keeps one row per source and sample identifier. Substrate rows must not count as independent bleaching measurements.

For each site and recorded date, we averaged distinct samples at each depth. We chose the shallowest and deepest endpoints within 1-20 m, with a gap of at least 3 m. We required known percentages in [0,100], coordinates and supplied heat values. We rejected site-date groups with coordinate spread above 0.01 degree, heat spread above 0.1 TSA_DHW unit, or more than one ocean. There were 1,683 pairs at 984 sites in 1998-2019. The median depth gap was 5 m.

The main count uses strictly positive values at both endpoints. Exact agreement means equality of parsed numbers after endpoint averaging. It is not equality within measurement error. No colony denominators or source precision limits are available.

Ocean samples have disjoint records. Year windows have disjoint years but can share sites. They use one monitoring system and are archive strata, not independent field replications. The design was exploratory and was set before inspection of the concordance summaries. See protocol.txt.

## Numerical agreement

There were 996 pairs with zero at both depths, 687 with at least one positive value, and 367 with two positive values. There were 1,052 exact matches in total; 996 (94.7%) were zeros. Of the last group, 56 had equal percentages (15.3%). Among all pairs with at least one positive value, the exact-agreement fraction was 8.2%. Averaging that fraction first within sites gives 8.3%. These denominators answer different questions.

| Ocean | Period | All pairs | Both positive | Exact positive | Exact rate | Random-pair reference |
|---|---|---:|---:|---:|---:|---:|
| Atlantic | 1998-2009 | 230 | 86 | 14 | 16.3% | 4.6% |
| Atlantic | 2010-2019 | 63 | 13 | 2 | 15.4% | 4.1% |
| Indian | 1998-2009 | 41 | 5 | 2 | 40.0% | 46.7% |
| Indian | 2010-2019 | 110 | 47 | 3 | 6.4% | 5.4% |
| Pacific | 1998-2009 | 536 | 109 | 20 | 18.3% | 9.2% |
| Pacific | 2010-2019 | 502 | 87 | 14 | 16.1% | 6.1% |

![Zero agreement](files/zero_agreement.png)

![Numerical agreement](files/agreement.png)

The random-pair reference preserves the observed shallow and deep positive values. It permutes deep values among both-positive pairs in each ocean and year, 2,000 times, with seed 1107. We report the mean match fraction. Singleton groups stay fixed. The CSV reports their counts and simulated 2.5 and 97.5 percentiles.

Atlantic and Pacific positive-match rates exceeded their random-pair reference means in both periods. Indian rates did not show the same pattern. This descriptive pattern does not test a shared mechanism across regions. The early Indian sample has only five positive pairs.

The reference destroys same-site pairing. It does not control local habitats, dates within a year, species, observers, or thermal history. Its spread is not a confidence interval for reefs. We give no p value. Random pairing is not a credible ecological null and cannot diagnose copied records.

The most frequent matched positive values were: 1% (11 pairs), 5% (10 pairs), 0.5% (7 pairs), 0.25% (6 pairs), 10% (6 pairs). Full frequencies are in matching_values.csv. Common rounded values can raise exact-match rates without shared reporting.

## Sensitivity and verification

Additional checks remove day-15 dates, remove values at 100%, restrict to one distinct sample per endpoint, or select supplied TSA_DHW of at least four. The last cutoff is descriptive, not a calibrated Coral Reef Watch threshold. All are selected subsets.

| Check | Both-positive pairs | Exact pairs | Rate |
|---|---:|---:|---:|
| Not day 15 | 355 | 55 | 15.5% |
| Both values below 100 | 366 | 56 | 15.3% |
| One sample per endpoint | 357 | 56 | 15.7% |
| Heat >= 4 | 38 | 3 | 7.9% |

An independent standard-library validator rebuilds endpoint means from raw distinct samples. It then checks pair and exact-match counts for every reported stratum. See validation.json. Earlier mean-depth calculations remain in estimates.csv as context, not the new result.

## Interpretation and limits

Most exact agreement came from zeros rather than repeated positive values. The result measures numerical agreement in complete selected records. Agreement does not establish equal susceptibility, temperature, or species responses. Shared exposure, community composition, rounded reports, a site-wide measure applied at both depths, and other reporting processes are possible explanations. The data do not identify which explanation applies. No error or misconduct is alleged.

Matching controls site, recorded date and broad survey source. It does not remove detection differences, missing outcomes, selective visits, or species and colony-size differences. Dates can be imputed. Repeated sites and common heat events make pairs dependent. We describe the finite archive rather than infer a rate for all reefs. Positive-only selection changes the target and is used only to remove zero agreement from this audit.

These observations cannot test mesophotic refuges. Bleaching is not death or biodiversity loss. The study does not measure air pollution or attribute a response to human-caused climate change. To distinguish explanations, future data should preserve depth-specific field sheets, observer information, precision rules, species, colony counts, light and underwater temperature.

## Reproduce

Use Python 3.12 with pandas, NumPy and Matplotlib. Tested versions are in audit.json. In an extracted writable bundle, run these three commands:

    python files/analyze.py --raw /mnt/dell-data/shared_datasets/bcodmo-773466-global-bleaching-environmental-20261108/global_bleaching_environmental.csv --out reproduced
    python files/concordance.py --pairs reproduced/matched_pairs.csv --out reproduced
    python files/plot_zero.py reproduced
    python files/validate.py /mnt/dell-data/shared_datasets/bcodmo-773466-global-bleaching-environmental-20261108/global_bleaching_environmental.csv reproduced

The first script checks the raw SHA-256. If the shared file is absent, retrieve https://datadocs.bco-dmo.org/file/B11vA82u7y2Owp/global_bleaching_environmental.csv to a private local path and use that path. Expected SHA-256: 78cc014b1e7887f26f4c44a40d4d9213212f3c6217541c6a1b69e723b61bfacb. Size: 16,772,400 bytes. Do not overwrite a shared dataset.

Exact shared alias: /mnt/dell-data/shared_datasets/bcodmo-773466-global-bleaching-environmental-20261108/global_bleaching_environmental.csv. The resolved immutable path is in audit.json. Source data use CC BY 4.0. Credit: Robert van Woesik, Deron Burkepile, Chelsey Kratochwill, BCO-DMO, Reef Check and contributing survey programmes. The baseline license applies subject to source rights. No new raw download was needed or shared data changed.

## Worker record

Campaign: 11_07_2026. Job: sci-1107-syam2-climate-pollution-biodiversity-77c6e125d367. Topic: climate-pollution-biodiversity. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort, through T3 Code and the Codex harness. Date: 2026-11-08. No agents were launched. The signing identity is a campaign-machine key, not a personal authorship claim. No private key is included. This publication is saved locally without remote archive or index submission.
