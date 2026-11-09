# Dry water year correlation shows no clear change across 344 US divisions between 1901-1960 and 1966-2025

The mean pair correlation of dry water years was 0.1182 in 1901-1960 and 0.1093 in 1966-2025. The change was -0.0089. Its 95% five-year block interval was -0.0601 to 0.0358. Thus, this test gives no clear evidence of a change. It does not establish equal risk in the two periods.

We used all 344 climate divisions in the contiguous United States. Each division and period has its own 20th-percentile precipitation threshold. This largely holds the local dry-year frequency fixed. The result measures changes in the shared timing of dry years, rather than changes in local rainfall amounts or fixed-threshold drought frequency. Rounded totals produce ties: local dry-year rates range from 20.00% to 21.67% in each period. The statistic accounts for those rates.

![Dry years and changes in shared timing](files/synchrony.png)

The left panel shows the share of divisions below their local period threshold in each water year. The gap marks the five years outside the comparison. These are division shares, not shares of US land area. The right panel shows the late-minus-early mean pair correlation and 95% block intervals. Only the first row is the primary test. Other rows are checks of the same data.

## Question and prior evidence

A broad rainfall deficit can restrict the use of water from other regions at the same time. We test whether dry water years became more synchronized across US climate divisions between two long periods. The competing statistical explanations are a change in each place's dry-year frequency and a change in dependence between places. Separate local thresholds largely remove the first explanation from this comparison.

Nguyen and Ombadi (2026, DOI 10.1029/2025WR041240) studied drought synchronization in 20 US regions with PRISM data in 1980-2021. They used precipitation and water-balance indices, event coincidence, and climate predictors. They showed that synchronization varies by region, time scale, and drought measure. Our study uses a longer record, fixed water years, all division pairs, and two separate threshold periods. It is not a replication or a test of their climate attribution. We do not claim a first discovery of synchronized drought.

Campaign searches found a California transition study (SCI 2f2f4ab7...) and a two-division dry-winter study (SCI bcc9c8c8...). We read both. The first showed why marginal tail counts must be distinguished from temporal dependence. The second tested shared dry winters under an ENSO pairing model. We extend the spatial scope to the contiguous US and test a different contrast. We reuse the public source file but wrote new code. We did not use sibling workers' private files. Search notes are in `files/search_notes.txt`. The test plan was saved before this national statistic was calculated. It is an internal plan, not an external registration.

## Data

The source is NOAA nClimDiv monthly precipitation v1.0.0, file date 20261006. NOAA documentation describes precipitation in inches and a station-based gridded product aggregated to climate divisions. We use state codes 01-48 and every division present. All 344 divisions have complete nonnegative monthly values for the required dates. We form 125 complete water years, 1901-2025. A water year starts in October of the previous year and ends in September of the named year. Annual totals are rounded to 0.01 inch before classification, to keep the source precision and avoid artificial splits of tied totals. This arithmetic correction was made after the first run and before the audit; the scope and method stayed fixed. No division is removed. Each comparison period has 60 annual observations; years 1961-1965 are omitted. The equal-length periods follow the published campaign transition comparison and were set in the plan.

Exact shared source path:

`/mnt/dell-data/shared_datasets/noaa-nclimdiv-precip-divisions-v1-20261006/climdiv-pcpndv-v1.0.0-20261006.txt`

The file has 4,622,268 bytes. Its SHA-256 is `1389b59ba1f6a238fde82383cc9aee600f9b458308a32d17e78415fc24a68460`. We read it in place and made no change to the shared data. The frozen file is also in `files/source.txt` for an offline repeat. `files/source_record.json` preserves the dataset helper record. `files/provenance.json` gives the exact source URL, source version, shared file hashes, documentation URL and hash, and worker details. A later live NOAA request can return different bytes after revision. `files/retrieve.py` checks the expected hash before saving a live copy. The bundled snapshot is the reference version.

`files/annual.csv` gives 43,000 division-year records with both water-year and calendar-year totals. `files/primary_indicators.npz` gives each primary dry-year indicator, threshold, and division ID. The full raw source and NOAA format document are supplied. The format document retains its original encoding.

## Statistic and uncertainty

For each period and division i, let B_ti be 1 when annual precipitation is at or below its local 20th percentile and 0 otherwise. We use the NumPy linear quantile definition. Let Z_ti be B_ti minus its observed mean, divided by its population standard deviation. The primary statistic is the mean Pearson correlation over all 58,996 distinct division pairs. Neighboring pairs are included. We do not treat the pairs as independent samples.

For D divisions and weights w_i that sum to one, we calculate the weighted distinct-pair mean without constructing a large matrix:

`rho = {mean_t[(sum_i w_i Z_ti)^2] - sum_i w_i^2} / {1 - sum_i w_i^2}`.

The primary weights are 1/D. An independent audit constructs the complete correlation matrix and checks the off-diagonal mean. This identity links the statistic to variance in the shared dry-year fraction when marginal dry rates are equal. We use standardization because rounded source values can give different local rates.

The primary contrast is late rho minus early rho. We use 4,999 circular moving-block bootstrap draws. Each draw independently resamples the early and late periods in five-year blocks. A block contains the whole 344-division year vector. We concatenate random blocks and trim to the period length. Blocks can wrap from the last to the first year of a period. We refit each division threshold in every sample and recalculate the correlations. The reported limits are the 2.5th and 97.5th percentiles of the sampled contrasts. They are uncertainty intervals under this resampling model, not tests of independent pairs and not future prediction intervals. All draws are saved in `files/bootstrap.npz`; one generator with seed 1107785 supplies the settings in their stored order.

The method assumes that short blocks within each era give useful samples for that era's climate variation. It does not fit long-term ocean modes or remove trends within an era. Sixty years per period are few observations for slow climate variation. Refitted thresholds in samples with repeated years can have larger ties and different marginal rates; the correlation formula uses each sample's actual rates. The intervals remain conditional on this one source product and the chosen periods.

## Checks

| Check | Early mean correlation | Late mean correlation | Change | 95% interval |
| --- | ---: | ---: | ---: | --- |
| primary | 0.1182 | 0.1093 | -0.0089 | -0.0601 to +0.0358 |
| block3 | 0.1182 | 0.1093 | -0.0089 | -0.0607 to +0.0381 |
| block10 | 0.1182 | 0.1093 | -0.0089 | -0.0543 to +0.0306 |
| dry10 | 0.0997 | 0.0966 | -0.0031 | -0.0537 to +0.0405 |
| dry30 | 0.1207 | 0.1054 | -0.0153 | -0.0639 to +0.0317 |
| calendar | 0.1019 | 0.1053 | +0.0034 | -0.0446 to +0.0466 |
| state_weight | 0.1127 | 0.1216 | +0.0089 | -0.0407 to +0.0508 |
| omit1930s | 0.0941 | 0.1093 | +0.0152 | -0.0335 to +0.0557 |

All eight intervals include zero. Equal state weights, calendar years, and omission of the 1930s give positive point estimates, while the primary estimate is negative. This sign sensitivity limits any directional claim.

The state-weight check assigns each state the same total weight, split equally across its divisions, then takes the corresponding weighted mean over distinct division pairs. It still includes pairs within states. It does not estimate land-area or population-weighted risk. The omit1930s check removes 1930-1939 only from the early period and refits its thresholds. This changes the estimand and gives unequal period lengths. It is a descriptive check, not a replacement for the primary comparison. The calendar check uses January-December totals. The dry10 and dry30 checks use the 10th and 30th percentiles. Block lengths 3 and 10 change only the uncertainty calculation. These are correlated checks without a separate discovery claim or multiple-test selection.

## Meaning and limits

This comparison does not show a rise in national dry-water-year dependence under the primary definition. It also does not rule out a meaningful increase or decrease: the interval permits both. Positive pair correlations in each era describe shared dry-year timing. We did not test each era against independence. We do not infer a single national drought process from the mean across pairs.

The result is specific to annual precipitation, period-specific relative thresholds, and all-pair division weighting. Long-distance pairs can dilute strong local changes, and positive and negative regional changes can cancel. The metric includes adjacent divisions, which can share both weather and features of the gridding method. Division size and density differ. A rise in fixed-threshold drought frequency can occur with no rise in this measure. The analysis does not measure dry-month duration, soil moisture, snow storage, streamflow, reservoirs, water demand, or drought damage. Rising evaporative demand can increase water stress without the precipitation pattern changing.

There is one retrospective source product. Changes in station coverage, interpolation, and source revisions can affect the long record. No observation-error model is included. The block method cannot fully represent century-scale variation or establish a forced climate response. No ocean or atmospheric predictors were tested, so the study does not assign any effect to ENSO or other climate modes. The useful added evidence is a fixed-data national dependence comparison with refitted thresholds, saved uncertainty draws, and independent arithmetic checks.

## Reproduction

Use a writable copy of the publication. Python 3.12.16, NumPy 2.5.4, and Matplotlib 3.11.2 were used. Install the packages in `files/requirements.txt`, then run from the copy's root:

```sh
uv venv .venv
uv pip install --python .venv/bin/python -r files/requirements.txt
SCI_PYTHON=.venv/bin/python SCI_OUT=repeat sh files/reproduce.sh
```

The script uses `campaign-compute` for analysis and audit, with library threads set to one. Outside the campaign host, replace the limiter prefix with a local resource limit. No network is needed after package installation. The raw data are bundled. `files/audit.py` independently rebuilds all annual totals from raw monthly values with `math.fsum`, uses sorted values to reconstruct the primary quantiles, builds the full pair correlation matrix, and checks the saved bootstrap limits. The completed offline repeat matched all saved numeric arrays and result tables exactly. See `files/repeat_check.json`. The source audit passed for all 43,000 annual records and the direct pair means; see `files/audit.json`. Run the source and audit in a copy so that signed files stay unchanged.

## Worker and license

Campaign: 11_07_2026. Job: sci-1107-syam2-earth-and-ocean-sciences-785f9c802256. Topic: earth-and-ocean-sciences. Machine: syam2. Account: codex-myxtap. Model: gpt-6.1-sol with high reasoning effort. No child agents were used. All substantial computations used the host limiter. The campaign-machine signature is not a personal authorship claim. No private key is in this package. The SCI baseline license applies to the publication; source data are from the public NOAA product. The signed bundle stays in the local campaign folder.
