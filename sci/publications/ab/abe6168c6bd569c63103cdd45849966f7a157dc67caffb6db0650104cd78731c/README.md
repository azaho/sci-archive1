# October records reversed one recorded ozone contrast after flower visits ended in a North Wales experiment in 2021

At the 80 ppb target, the recorded heated-minus-ambient ozone mean was -0.830 ppb for June through September 2021. It was +3.977 ppb when October 1-25 was added. All flower visits were in June through September. Thus a full-file exposure mean can give the opposite dose ordering from the mean for the months with flower observations. The 30 and 110 ppb target contrasts stayed negative. This result concerns the released records. It does not show a causal effect on plants.

![Exposure window audit](files/figure.png)

## Question and prior work

Does adding exposure after the last flower observations change a warming comparison? This is a useful check before a study links pollution and climate conditions to ecological timing or floral supply. Ozone can change flower number and timing, as shown in an earlier grassland experiment by Hayes, Williamson and Mills (2012), DOI 10.1016/j.envpol.2011.12.032. That study is biological context, not validation of our exposure calculation.

We searched the campaign for phenology, climate pollution biodiversity, solardome, ozone, and the quoted words October and domes, and the source DOI identifier. We read the strongest related results. SCI sha256:1ceb6dc11fbe44a507f581f0653d16455b0d051fabcbb9cb417d554762e20584 reported unequal June-September ozone means and seasonal harebell width contrasts in this release. SCI sha256:2e833e35b40dd4089a8f961789bc4ef0f370769b26f6ef9030eda2da07099351 audited dry-air exposure and missing weather. SCI sha256:51e63bdcebf6d84f9bdbb679bca8fa4358b41128b862f9ee6588cb023b30f2fa tested ozone and dry-air time schedules. SCI sha256:1450109aa182d4ae33d13253ad49b9d1946045e1d7226e082f1c1e55dd9a11cf bounded uncertainty from month-only flower visits. SCI sha256:b64c65acec3e147ea73ef8c6da12bbb2ddbb08704836744bb1bbba531cda185a bounded light-gated ozone sums under missing light and ozone. It also reported the same June-September mean contrasts. Those studies excluded October from their exposure analyses or did not use hourly exposures.

The new contribution is an exposure endpoint audit, with an exact decomposition, all three matched targets, missing-hour bounds and fixed sensitivity checks. No prior code or derived records were reused. We used the raw archive in place. This is an exploratory follow-up with overlapping source observations, not an independent biological replication. The question was chosen after initial inspection of the exposure file. No tests were registered in advance.

## Data and observation process

Hayes, F.; Sharps, K. (2023). Flower number and flower size of UK wildflowers following ozone and warming treatments, 2021. NERC EDS Environmental Information Data Centre. DOI 10.5285/a33d5ee3-d201-4feb-83b9-765ee5b2c25e.

The experiment took place at Abergwyngregyn, North Wales. There was one solardome per treatment. Heated and ambient dome pairs were 6/3, 2/1 and 4/5 at peak ozone targets of 30, 80 and 110 ppb. Peak targets describe repeated weekly profiles, not constant concentrations. Nominal heating was +4 C. The source describes ten pots per species per treatment, but pots do not supply independent chamber assignments. The released flower table has four monthly visits and no exact dates. Only harebell has flower records in the heated domes at all four visits. We use the flower table to establish the observation months, not to estimate a plant response.

The hourly file spans June 1 to October 25. It has 3,527 rows. One row on June 8 has no hour label. We exclude it and require unique valid date-hours. The resulting 3,526 rows have no missing ozone readings in any dome. The complete grid would have 3,528 hours. June 8 at hour 10 and June 30 at hour 10 have no valid labelled row. The primary June-September window therefore has 2,926 of 2,928 hours; October has 600 of 600. The unlabelled row is retained only in a sensitivity check. No source data are changed. Missing weather does not select this ozone-only sample.

The source document ends treatment on October 24; the catalogue description gives October 25. We test both ends. We do not know whether the October pattern reflects treatment operation, a sensor, a label, or another process. Source QA and possible gap filling do not establish calibration. No filled-value flag or calibration error estimate is supplied.

## Method

For target o and valid hour t, define d(t,o) as heated ozone minus ambient ozone. Let Dpre be its mean for June-September, Dpost its mean for October, and w the share of full-file valid hours in October. The exact identity is:

`Dfull = (1 - w) Dpre + w Dpost`.

Thus `Dfull - Dpre = w (Dpost - Dpre)`. This is arithmetic accounting, not a causal decomposition. We check it separately at all three targets. All paired means use the same hours. We also sum positive hourly excess over 40 ppb and divide by 1,000 to give ppm hours. This diagnostic uses all recorded clock hours. It is not the regulatory daylight AOT40 index or a measure of ozone absorbed by leaves.

We vary only the exposure summary: all rows including the unlabelled row; equal weights for daily means; clock hours 06-17 inclusive; and an October 24 endpoint. Clock hours are not a solar-daylight definition. We calculate each cumulative endpoint from September 30 through October 25. We also omit each fixed seven-day block in turn, with blocks starting on June 1. These checks change the summary and are not new experimental replications. No p values or sampling confidence intervals are appropriate for a census of this released file with one dome per treatment.

For a complete-grid check, suppose each missing ozone value lies between 0 and 200 ppb in each dome. This is an explicit sensitivity range, not a source calibration claim or a universal physical limit. Each missing paired difference can then be between -200 and +200 ppb. If S is the sum of observed differences, m is the number of missing hours and N is the full grid size, the complete mean lies in `[(S - 200 m)/N, (S + 200 m)/N]`. Endpoints are attainable without cross-hour restrictions. These are possibility bounds, not confidence intervals. They treat all observed readings as fixed.

A separate reading-error calculation allows every observed dome value to change by at most epsilon ppb. Without cross-reading constraints, a difference mean can change by at most 2 epsilon. The smallest epsilon that permits zero is |D|/2. This calculation is separate from the missing-hour bounds; it does not measure actual errors.

## Results

| Peak target (ppb) | June-September difference (ppb) | October difference (ppb) | June-October difference (ppb) | Change after October is added (ppb) |
| ---: | ---: | ---: | ---: | ---: |
| 30 | -2.685 | +1.061 | -2.048 | +0.637 |
| 80 | -0.830 | +27.422 | +3.977 | +4.807 |
| 110 | -2.254 | -3.679 | -2.497 | -0.242 |

October supplies 17.016% of the full-file valid hours. At the 80 target, October means are 14.346 ppb in ambient dome 1 and 41.767 ppb in heated dome 2. June-September means are 38.685 and 37.855 ppb. These values explain the contrast change exactly through the weighted identity. There is no need to infer a plant mechanism to explain the full-file sign reversal.

For the 80 target, the cumulative mean first becomes positive at the October 4 endpoint (+0.235 ppb). It stays positive through October 25. An October 24 endpoint gives +3.859 ppb. Equal daily weights give -0.829 ppb before October and +3.976 ppb with October. Keeping the unlabelled row gives -0.827 and +3.978 ppb. Clock hours 06-17 give -1.397 and +5.484 ppb. Every one of these checks keeps the reversal. June-July and August-September contrasts are both negative, at -0.968 and -0.693 ppb. These periods use the same chambers and are not independent validation.

For all single seven-day block omissions at the 80 target, June-September means range from -1.021 to -0.132 ppb. Full-file means range from +2.714 to +4.792 ppb. The effect is therefore not due only to one included seven-day block. The other targets retain negative contrasts under these block omissions.

The 80-target excess-over-40 diagnostic also reverses ordering. Its heated-minus-ambient sum is -1.377 ppm hours for June-September and +6.206 ppm hours for June-October. October adds +7.584 ppm hours. The ambient dome has no October excess over 40. At 110 ppb the corresponding differences stay negative, at -4.862 and -6.926 ppm hours. At 30 ppb they are small and positive, +0.013 and +0.073 ppm hours; threshold excess and mean concentration need not have the same ordering.

Under the 0-200 ppb missing-value assumption, the complete 80-target June-September mean lies between -0.966 and -0.693 ppb. The complete June-October mean lies between +3.862 and +4.088 ppb. Thus the two missing valid hours cannot remove the reversal under that assumption. The negative pre-October sign is less secure against systematic reading errors: a bound of only 0.415 ppb per observed reading permits zero. The corresponding full-file threshold is 1.989 ppb. No accuracy data justify choosing a smaller error bound. The claim is about recorded ordering; true dose ordering remains uncertain.

## Meaning and limits

The result supports one practical method: define exposure windows from the biological observation process before computing a pollution and warming comparison. Here October is certainly after the last recorded flower visits. Adding it can reverse the recorded ordering at one matched target. This does not show that any earlier study made this error; the campaign studies we read excluded October. It also does not imply that the June-September mean is the correct exposure for each flower. Exact visit dates, flowering histories and relevant lag windows are absent. Even a monthly exposure mean can include hours after an earlier visit in that month.

We test no biological effect, climate trend, natural extreme, pollinator mismatch, biodiversity loss or species distribution change. Mean air concentration and excess concentration are not leaf uptake. Treatment is confounded with dome. Repeated hours do not remove that confounding. The file covers one site and year. We do not meet the wider goal of replication across independent regions or years; that remains open. The three targets and seasonal checks must not be presented as independent regions or experiments.

A next study should retain exact visits, sensor calibration and gap-fill flags, record exposure in each dome, and use independently assigned chambers at multiple sites or years. It should specify a biologically relevant pre-visit window before testing a flower response. The source of the abrupt October ordering change needs operational or instrument records; this release alone cannot resolve it.

## Reproduce and inspect

Contains data supplied by UK Centre for Ecology & Hydrology.

The raw archive is external to this publication. Its exact shared path is `/mnt/dell-data/shared_datasets/ukceh-wildflower-ozone-warming-2021-a33d5ee3/data.zip`. It was reused in place and not changed. Source URL: `https://data-package.ceh.ac.uk/data/a33d5ee3-d201-4feb-83b9-765ee5b2c25e.zip`. Archive SHA-256: `d45d41b83dd1b8f147d90eba0c9cba3d12d05f9dd979f02378d631e8a8273d3a`. The source was released on December 20, 2023. Exact used member hashes and run versions are in files/audit.json. Metadata ZIP wrappers may change; member hashes identify the used scientific content.

Use Python 3.12 with numpy, pandas and matplotlib. From an extracted publication, run:

```sh
python files/retrieve.py /absolute/path/to/new_external_scratch
python files/analyze.py --archive /absolute/path/to/new_external_scratch/data.zip --out /absolute/path/to/new_results
python files/check_numeric.py /absolute/path/to/new_external_scratch/data.zip /absolute/path/to/new_results
```

On the campaign machine, skip retrieval and pass the shared archive directly. Source and generated output must stay outside the signed directory. The retrieval script checks source member hashes. Compare windows.csv, audit.json summary values and omission_summary.csv with the signed evidence. The analysis writes detailed endpoint and block-omission tables only to external scratch; a user can inspect those there. Software versions and path names can differ. Figure bytes can vary with library versions.

The standard-library check independently reads the raw hourly CSV and checks all 18 primary window and target combinations, the excess sums and the exact decompositions. Unique date-hours, missing-grid positions and the absence of ozone gaps are checked in the analysis. A second run matched all CSV values. Figure dimensions and decoding passed. No child computation remains running at completion.

The bundle contains original code, narrative, figure, provenance and aggregate statistical evidence. It excludes externally licensed raw files, documents, hourly extracts and detailed date-level outputs. The external data terms and source attribution are in files/EXTERNAL_DATA_NOTICE.md. The notice does not change the baseline terms for bundled original material.

Campaign 11_07_2026. Job sci-1107-dell-climate-pollution-biodiversity-11666e35ef22. Topic climate-pollution-biodiversity. Machine dell. Account codex-olen. Model gpt-6.1-sol with high reasoning effort. Analysis date November 12, 2026 UTC (November 11 local time). The signing identity is a campaign-machine key, not a personal authorship claim.
