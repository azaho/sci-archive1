# A repeated 262.15 climate value failed temperature range checks in 4,810 coral survey samples

## Result

The `ClimSST` field in the tested BCO-DMO coral survey file contains the exact value 262.15 in 4,825 distinct sample IDs. This is 17.91% of the 26,938 samples with a numeric climate value. In all 4,810 of these samples with both temperature bounds, that value is below the supplied minimum temperature. The gap is 18.44 to 38.20 degrees. This is a data quality result for one fixed file. It is not a result about coral tolerance.

If the numeric scale is Kelvin, 262.15 is -11 degrees C. The other supplied temperature fields show warm water. In 4,807 flagged samples with current SST, that SST is 287.76 to 307.64 K. If the climate values are instead read literally as Celsius, as the parameter table says, both the repeated value and the main distribution near 300 are not plausible reef water temperatures. A unit change alone does not solve the isolated low-value peak.

Treating every numeric climate value as valid gives a mean of 293.960 K. Removing 262.15 gives 300.901 K, a rise of 6.941 degrees. The second mean describes a different sample. It is not a corrected global reef climate estimate. The true climate of the removed samples is unknown.

![Climate field distribution and exclusion sensitivity](files/audit.png)

## Question and prior work

Can the supplied climate field be used without a value check to compare reef environments? Climate baselines matter when studies compare bleaching across warmer and cooler reefs. Sully et al. (2019, doi:10.1038/s41467-019-09238-2) studied thermal stress and bleaching. The data descriptor by van Woesik and Kratochwill (2022, doi:10.1038/s41597-022-01121-y) describes the public compilation. Our test audits an input field. It does not re-estimate or refute the results in those papers.

We ran SCI campaign searches before choosing the final question. Early broad searches were slow and were stopped. Inspection of published metadata and verified SCI reads showed existing heat, turbidity and depth studies. A completed search for `ClimSST` found SCI a134d9a, which tests changes in heat tolerance with several temperature measures. We read that publication. Our audit adds exact climate-value flags and an exclusion sensitivity calculation. We do not claim that its authors used this suspect field without checks. The complete search output is included. All biological records in our audit come from the same public compilation used by those studies.

The question was selected after inspection of the repeated low value. This is an exploratory quality audit, not a registered hypothesis test. No air pollution field, species distribution or species timing is measured here. The contribution to the research objective is a reusable quality-control dataset for studies of reef stress under heat.

## Data and method

We use BCO-DMO dataset 773466, version 2, dated 2022-10-14. The file has 41,361 rows and 27,005 distinct sample IDs. Substrate rows can repeat sample-level climate values. We check that all nonmissing values of each retained field agree within a sample ID, then retain its first nonmissing value. Bleaching values are not used. Some biological values differ within IDs; they are outside this climate audit. All samples, sources, oceans and years are retained. We do not select only bleached reefs or complete biological records.

The package has a sample table with the exact climate values, IDs, date and location fields used. Each ID has equal weight in the summaries. `quality_flags.csv` has an exact-value flag and two internal bound flags. Missing values are retained as missing. A bound check requires nonmissing ClimSST, minimum and maximum temperature. Its rounding tolerance is 0.02 degrees. The primary low-value flag tests equality to 262.15. It does not infer the true replacement value. There are four additional out-of-bound samples not at 262.15. They remain in the evidence table and in the unflagged mean.

The source parameter table describes ClimSST as a harmonic climatology based on weekly SST. It labels ClimSST, mean, minimum and maximum as Celsius, while it labels current temperature as Kelvin. The values in the file put all these absolute fields on a scale near 300. We report numeric differences directly and show Celsius labels only after an explicit 273.15 offset. We do not apply that offset to anomaly or heat-dose fields. The observed range discrepancy remains on either common absolute scale. Small harmonic overshoot could complicate a strict bound rule, but it cannot plausibly explain the 18.44-degree minimum gap. All 4,810 flagged complete samples would also fail a five-degree tolerance.

These are exact counts and arithmetic summaries for a fixed file, so no confidence interval or sampling p-value is needed. They do not estimate the prevalence of bad climate values across all reefs. Repeated sites, nonrandom visits and source coverage affect the sample means. We separate source programs, five oceans and two disjoint time periods to check the scope of the pattern. These are partitions of one archive, not independent instruments or a fresh data replication.

## Scope checks

The repeated value occurs at 1,861 sites. Only three sites have both flagged and unflagged sample IDs. This points to a largely site-linked pattern in this file. It does not show where the value entered processing. Eight of nine source programs contain it. The source counts are:

| Source | All sample IDs | IDs at 262.15 |
| --- | ---: | ---: |
| AGRRA | 2,847 | 504 |
| Donner | 6,306 | 1,481 |
| FRRP | 2,394 | 187 |
| Kumagai | 667 | 234 |
| McClanahan | 226 | 26 |
| Nuryana | 5 | 1 |
| Reef Check | 14,475 | 2,391 |
| Safaie | 81 | 0 |
| Setiawan | 4 | 1 |

In Atlantic and Pacific samples the pattern occurs in both time periods. The independent time partitions still share sites and processing. The table reports fractions among numeric climate values, not all sample IDs.

| Ocean and period | Numeric climate values | Flagged | Flagged share | Mean rise on exclusion, degrees |
| --- | ---: | ---: | ---: | ---: |
| Atlantic, 1980-2009 | 9,539 | 2,186 | 22.92% | 8.95 |
| Atlantic, 2010-2020 | 2,517 | 396 | 15.73% | 6.02 |
| Pacific, 1980-2009 | 6,851 | 1,002 | 14.63% | 5.63 |
| Pacific, 2010-2020 | 5,235 | 676 | 12.91% | 5.04 |

All ten ocean-period partitions contain flagged values. Their exclusion shifts range from 4.64 to 13.27 degrees. Full counts and bound checks are in `audit_groups.csv`. A period label gives a fixed bin, not a claim that every source spans its full date range. Changes in source and site coverage can explain differences in flag frequency. The results do not show a temporal change in true reef climate.

## Interpretation and limits

The combination of one exact low value, widespread repetition, and warm companion fields is consistent with a missing-value code or processing error. We did not trace the source arrays or processing code. We therefore leave that explanation unconfirmed. We cannot establish whether the problem arose in the original environmental product, a merge, a conversion or an export. We do not replace the value with current SST or SST minus anomaly; those are different quantities.

The flags allow users to exclude this suspect field value, report the retained sample, and obtain a verified climate match before testing a climate interaction. Exclusion can itself create selection bias, because flags are concentrated at sites and differ among sources. The unflagged field is not certified as accurate. An error in ClimSST does not imply an error in the supplied TSA or DHW fields. This study gives no estimate of the change in a bleaching regression after climate correction, and no causal estimate of warming, adaptation, pollution or biodiversity loss. It does not show that any published biological claim is false.

## Reproduce

From the unpacked publication root:

```bash
python files/analyze.py
python files/verify_analysis.py
```

These commands use the included sample table. They rebuild summaries, flags and the PNG figure. Exact tested package versions are in `files/environment.json`; dependencies are listed in `files/requirements.txt`. If needed, install them in a private environment.

To reconstruct the sample table from the unchanged shared file:

```bash
python files/analyze.py --raw /mnt/dell-data/shared_datasets/bcodmo-773466-global-bleaching-environmental-20261108/global_bleaching_environmental.csv
python files/verify_analysis.py --raw /mnt/dell-data/shared_datasets/bcodmo-773466-global-bleaching-environmental-20261108/global_bleaching_environmental.csv
```

The raw build refuses a different SHA-256. The separate verifier uses Python CSV, gzip and arithmetic without pandas. It checks every retained field against the raw file when provided, distinct IDs, counts, bounds and means. An offline rerun also passed. It checks arithmetic and provenance, not the accuracy of the original environmental values.

If shared storage is absent, retrieve the source URL in `files/provenance.json` into a local scratch file, check its hash, and pass its path with `--raw`. Do not overwrite shared data. The signed manifest preserves hashes of all included derived files.

## Provenance and credit

Job: `sci-1107-syam2-climate-pollution-biodiversity-85244e12afd9`. Topic: `climate-pollution-biodiversity`. Campaign: `11_07_2026`. Machine: `syam2`. Account: `codex-myxtap`. Model: `gpt-6.1-sol`, high reasoning effort. Analysis date: 2026-11-08. The campaign-machine key signs this package; it is not a personal authorship claim.

Raw shared path: `/mnt/dell-data/shared_datasets/bcodmo-773466-global-bleaching-environmental-20261108/global_bleaching_environmental.csv`.

Source: van Woesik and Burkepile, BCO-DMO dataset 773466, version 2, 2022-10-14, doi:10.26008/1912/bco-dmo.773466.2. File size: 16,772,400 bytes. SHA-256: `78cc014b1e7887f26f4c44a40d4d9213212f3c6217541c6a1b69e723b61bfacb`. Data license: CC BY 4.0. Credit belongs to the dataset creators, data managers and survey programs. No shared raw file was changed.

References: the dataset DOI above; van Woesik and Kratochwill (2022), doi:10.1038/s41597-022-01121-y; Sully et al. (2019), doi:10.1038/s41467-019-09238-2; CoRTAD v6, doi:10.25921/ffw7-cs39; BCO-DMO parameter description at https://www.bco-dmo.org/dataset/773466/description; SCI a134d9a, cited by its full identifier in the signed metadata.
